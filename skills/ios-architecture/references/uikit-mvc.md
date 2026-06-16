# UIKit MVC

Use UIKit MVC for UIKit-first apps and screens where `UIViewController` can
remain a screen coordinator instead of becoming a business-logic container.
Apple's UIKit model-view-controller guidance makes the view controller the
intermediary between view objects and data/model objects; keep that role narrow.

Relevant Apple docs:

- `UIViewController`: https://sosumi.ai/documentation/uikit/uiviewcontroller
- Displaying and managing views with a view controller: https://sosumi.ai/documentation/uikit/displaying-and-managing-views-with-a-view-controller
- `loadView()`: https://sosumi.ai/documentation/uikit/uiviewcontroller/loadview%28%29

## Contents

- [Default Shape](#default-shape)
- [Responsibilities](#responsibilities)
- [Example Screen](#example-screen)
- [App Shell and Feature Factories](#app-shell-and-feature-factories)
- [Assembly and Dependency Injection](#assembly-and-dependency-injection)
- [Collections and Delegates](#collections-and-delegates)
- [Navigation](#navigation)
- [When to Escalate](#when-to-escalate)
- [Review Checklist](#review-checklist)

## Default Shape

For simple UIKit features, start with this structure:

```text
Modules/
+-- MainFlow/
|   +-- HomeScreen/
|   |   +-- Controller/
|   |   |   +-- HomeController.swift
|   |   +-- View/
|   |   |   +-- HomeView.swift
|   |   +-- Model/
|   |       +-- HomeItem.swift
+-- TabBar/
|   +-- TabBarController.swift
|   +-- TabBarControllersFactory.swift
+-- Extra/
|   +-- ActivityIndicatorScreen/
Classes/
+-- Navigation/
|   +-- NavigationController.swift
Common/
+-- UI/
+-- Models/
+-- Managers/
+-- Services/
+-- Network/
+-- Extensions/
+-- Helpers/
```

The key split:

- `Modules/{Flow}/{Feature}Screen`: user-facing features grouped by app flow,
  such as intro, main, private area, paywall, or settings.
- `Controller`: UIKit lifecycle, target/action, delegate/data-source wiring,
  screen state, navigation decisions.
- `View`: subview creation, layout constraints, visual state setters, reusable
  UI components. It does not fetch data or navigate.
- `Model`: value types and display/domain data used by the screen.
- `Common/UI`: reusable UIKit views, collection cells, buttons, headers, and
  base view classes used across feature modules.
- `Manager` or `Service`: business operations, persistence, crypto, network,
  reachability, cache access.
- `Classes/Navigation`: app-wide navigation subclasses and navigation bar
  customization. Keep feature-specific routing out of these subclasses.
- `Assembly` or factory: constructs controllers, tab roots, or flow roots and
  injects dependencies.

## Responsibilities

### Controller

Keep these in the controller:

- `loadView()` assigning a custom root view when building UI in code.
- `viewDidLoad()`, `viewWillAppear(_:)`, and lifecycle coordination.
- Target/action wiring for buttons, controls, refresh controls, and text fields.
- Table/collection view data source and delegate methods for screen-owned lists.
- Mapping manager/service results into screen state and calling view update
  methods.
- Pushing, presenting, or replacing controllers for local navigation.

Move these out of the controller:

- Raw network calls.
- Keychain/UserDefaults/storage internals.
- Crypto/signing/encryption details.
- Large date/number formatting policies reused across screens.
- Complex domain decisions or multi-step workflows.
- Layout constraints that belong in a custom `UIView`.

### View

Use a custom `UIView` when the screen is programmatic. If the project uses
SnapKit, make SnapKit the default constraint style instead of raw Auto Layout
anchors.

```swift
import SnapKit
import UIKit

final class HomeView: UIView {
    let collectionView = UICollectionView(frame: .zero, collectionViewLayout: UICollectionViewFlowLayout())
    let refreshControl = UIRefreshControl()

    override init(frame: CGRect) {
        super.init(frame: frame)
        addViews()
        setupConstraints()
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    private func addViews() {
        addSubview(collectionView)
        collectionView.refreshControl = refreshControl
    }

    private func setupConstraints() {
        collectionView.snp.makeConstraints { make in
            make.edges.equalToSuperview()
        }
    }
}
```

Then install it from the controller:

```swift
final class HomeController: UIViewController {
    private let mainView = HomeView()
    private let userManager: UserManagerProtocol
    private var items: [ActivityModel] = []

    init(userManager: UserManagerProtocol) {
        self.userManager = userManager
        super.init(nibName: nil, bundle: nil)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func loadView() {
        view = mainView
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        configureActions()
        configureCollectionView()
        fetchData()
    }
}
```

When overriding `loadView()` for programmatic UI, assign `view` directly and do
not call `super.loadView()`.

SnapKit rules:

- Use `snp.makeConstraints` for first-time setup.
- Use `snp.updateConstraints` when only constants change.
- Use `snp.remakeConstraints` only when the whole constraint set changes.
- Keep SnapKit calls in the custom view, cell, or reusable UI component, not in
  the controller, unless the controller owns a container-level layout decision.
- Prefer `make.edges.equalToSuperview().inset(...)`,
  `make.center.equalToSuperview()`, and `make.size.equalTo(...)` for readable
  constraints.
- In reusable UI components, expose state with setters, properties, or Combine
  publishers, but keep the subscription and constraint updates inside the view.

For a reusable header or cell that changes its entire constraint shape, use
`remakeConstraints` deliberately:

```swift
final class HeaderView: UICollectionReusableView {
    var contentInsets: UIEdgeInsets = .zero {
        didSet { updateContentInsets() }
    }

    private let contentView = UIView()

    private func updateContentInsets() {
        contentView.snp.remakeConstraints { make in
            make.top.equalToSuperview().inset(contentInsets.top)
            make.bottom.equalToSuperview().inset(contentInsets.bottom)
            make.leading.equalToSuperview().inset(contentInsets.left)
            make.trailing.equalToSuperview().inset(contentInsets.right)
        }
    }
}
```

## Example Screen

A good UIKit MVC controller can own simple screen state:

```swift
private var selectedFilter: ActivityFilter = .all
private var allItems: [ActivityModel] = []

private var visibleItems: [ActivityModel] {
    switch selectedFilter {
    case .all:
        return allItems
    case .authorized:
        return allItems.filter { $0.loginState == .success }
    case .failed:
        return allItems.filter { $0.loginState.isFailure }
    }
}
```

This is still MVC when:

- The state is only for one screen.
- Filtering is simple presentation logic.
- Data loading is delegated to `UserManagerProtocol` or another dependency.
- Cells receive value models and do not reach into services.

Escalate when this grows into complicated state transitions, shared state, or
business rules that need standalone tests.

## App Shell and Feature Factories

For tab-based UIKit apps, keep the root shell explicit:

```swift
enum TabBarView {
    case home
    case privateArea
    case settings
}

protocol TabBarControllersFactoryProtocol {
    func buildView(for type: TabBarView) -> UIViewController
}

final class TabBarControllersFactory: TabBarControllersFactoryProtocol {
    func buildView(for type: TabBarView) -> UIViewController {
        let controller: UIViewController = switch type {
        case .home:
            HomeController()
        case .privateArea:
            PrivateAlbumController()
        case .settings:
            SettingsController()
        }

        controller.tabBarItem = buildTabBarItem(for: type)
        return NavigationController(rootViewController: controller)
    }
}
```

Use this shape when:

- The tab bar owns root tab composition, visual tab items, and tab ordering.
- Each tab root is wrapped in a shared `NavigationController`.
- A special tab needs a specialized navigation subclass for authentication,
  privacy, or gesture behavior.
- The `UITabBarController` should stay focused on installing controllers,
  tab bar appearance, haptics, and tab-selection events.

Keep the boundary clean:

- The tab factory may build root controllers and inject app-level dependencies.
- The tab factory should not fetch data, start scanners, or decide screen
  content.
- Navigation subclasses may own navigation bar class, gesture policy, and
  push/pop mechanics.
- Navigation subclasses should not know feature business rules except narrow
  app-shell gates such as "authenticate before opening this tab."

## Assembly and Dependency Injection

Prefer constructor injection for controllers:

```swift
protocol UserManagerProtocol {
    func getLatestActivity() async -> Result<[ActivityModel], Error>
}

enum HomeAssembly {
    static func make() -> UIViewController {
        HomeController(userManager: DI.ManagersAssembly.userManager)
    }
}
```

A simple static assembly is acceptable for small UIKit apps. Keep it as the
composition root; do not call global singletons from every controller when a
constructor parameter would make the dependency visible and testable.

Singletons are acceptable at app boundaries for truly shared services such as
cache, analytics, subscription state, or photo-library permission state. Hide
them behind protocols when feature code needs tests or when a controller would
otherwise reach through several global objects.

Use protocols for dependencies that cross external boundaries or need tests:

- Network-backed managers.
- Persistence/cache services.
- Reachability/location/auth services.
- Feature factories and routers.

Do not create protocols for every view or model by default.

Do not let display models or enum cases reach into managers directly. If a
model needs manager-derived state, compute that state in the controller,
factory, or service and pass a value into the model.

## Collections and Delegates

For table and collection views:

- Register cells in one setup method.
- Keep cell configuration value-based: `cell.model = items[indexPath.item]`.
- Keep delegate callbacks as UI events; call manager/service methods from the
  controller or a small action method.
- Use `weak` delegates in cells to avoid retain cycles.
- Move repeated cell sizing/layout rules into cell or layout helpers when they
  are reused.

```swift
extension HomeController: UICollectionViewDataSource, UICollectionViewDelegate {
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        visibleItems.count
    }

    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell: ActivityCollectionCell = collectionView.dequeueReusableCell(for: indexPath)
        cell.model = visibleItems[indexPath.item]
        return cell
    }
}
```

## Navigation

For simple UIKit apps, controller-local navigation is acceptable:

```swift
private func showScanner() {
    let controller = ScanQRController(authManager: DI.ManagersAssembly.authManager)
    controller.hidesBottomBarWhenPushed = true
    navigationController?.pushViewController(controller, animated: true)
}
```

Use a factory or coordinator when:

- Multiple controllers need to build the same destination.
- Navigation depends on authentication/onboarding state.
- You need deep links or reusable flow transitions.
- Tests need to verify routing without presenting real controllers.

## When to Escalate

Stay with UIKit MVC when:

- The controller is mostly lifecycle, actions, delegate wiring, and simple
  screen state.
- Managers/services own network, persistence, crypto, and business operations.
- The custom view owns layout and visual state.
- The feature has one or two destinations and local navigation is clear.

Move toward MVVM when:

- Formatting, validation, and display state become large enough to test
  separately.
- Several views reuse the same transformed state.
- Controller tests are hard because too much state calculation lives there.

Move toward Coordinator/Router when:

- Navigation becomes cross-feature or conditional.
- Multiple flows share destination construction.
- Deep links must enter the flow at different points.

Move toward Clean Architecture when:

- Domain rules matter independently of UIKit.
- Use cases span multiple managers/services.
- Data mapping and business policies need long-lived boundaries.

## Review Checklist

- [ ] `UIViewController` owns lifecycle, UI event wiring, simple screen state,
      and local navigation only.
- [ ] Custom `UIView` owns layout and visual subviews.
- [ ] SnapKit constraints live with the custom view, cell, header, or reusable
      UI component that owns the layout.
- [ ] Managers/services own network, persistence, crypto, reachability, and
      cache access.
- [ ] Dependencies are visible through initializers or feature assemblies.
- [ ] Collection/table cells receive value models and use weak delegates.
- [ ] Display models and enum cases do not read global managers directly.
- [ ] Screen state does not leak into global singletons.
- [ ] Business rules that need tests are outside the controller.
- [ ] Tab roots and shared navigation wrappers are built by an app-shell
      factory, not scattered across feature controllers.
- [ ] Navigation is local and obvious, or moved into a factory/coordinator.
- [ ] `loadView()` is used correctly for programmatic UI.
- [ ] The feature has a clear escalation path if MVC starts to become massive.
