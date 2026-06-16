# UIKit Lifecycle and Layout

Use this reference when building or reviewing `UIViewController`, custom
`UIView`, Auto Layout, SnapKit, and child view-controller containment.

Official docs:

- `UIViewController`: https://sosumi.ai/documentation/uikit/uiviewcontroller
- Displaying and managing views with a view controller: https://sosumi.ai/documentation/uikit/displaying-and-managing-views-with-a-view-controller
- `UIView`: https://sosumi.ai/documentation/uikit/uiview

## Contents

- [Lifecycle Placement](#lifecycle-placement)
- [Custom Root Views](#custom-root-views)
- [Auto Layout and SnapKit](#auto-layout-and-snapkit)
- [Child View Controllers](#child-view-controllers)
- [Checklist](#checklist)

## Lifecycle Placement

| Method | Use for |
| --- | --- |
| `viewDidLoad` | One-time setup: subviews, constraints, delegates, data sources, registrations |
| `viewIsAppearing(_:)` | Geometry/trait-dependent updates before the view is visible |
| `viewWillAppear(_:)` | Transition-coordinated changes and balanced observer setup |
| `viewDidLayoutSubviews()` | Lightweight layer frame updates only |
| `viewDidAppear(_:)` | Start visible-only work such as animations or analytics |
| `viewWillDisappear(_:)` / `viewDidDisappear(_:)` | Cancel visible-only tasks, timers, and transient work |

Do not read final bounds, safe-area dependent geometry, or collection view
layout attributes in `viewDidLoad`.

## Custom Root Views

```swift
final class ProfileController: UIViewController {
    private let mainView = ProfileView()

    override func loadView() {
        view = mainView
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        configureActions()
        configureCollectionView()
    }
}
```

When overriding `loadView()`, assign `view` directly and do not call
`super.loadView()`.

## Auto Layout and SnapKit

Native Auto Layout rules:

- Set `translatesAutoresizingMaskIntoConstraints = false` for programmatic
  views.
- Activate constraints in batches with `NSLayoutConstraint.activate`.
- Keep references to constraints whose constants or active state change.
- Avoid changing priority to or from `.required` at runtime.

SnapKit rules:

- Use `snp.makeConstraints` once during setup.
- Use `snp.updateConstraints` for constant changes.
- Use `snp.remakeConstraints` only when the entire layout shape changes.
- Keep SnapKit inside the view, cell, or reusable component that owns layout.

```swift
final class ProfileView: UIView {
    let avatarView = UIImageView()
    let nameLabel = UILabel()

    override init(frame: CGRect) {
        super.init(frame: frame)
        addSubview(avatarView)
        addSubview(nameLabel)

        avatarView.snp.makeConstraints { make in
            make.top.equalTo(safeAreaLayoutGuide).offset(16)
            make.centerX.equalToSuperview()
            make.size.equalTo(96)
        }

        nameLabel.snp.makeConstraints { make in
            make.top.equalTo(avatarView.snp.bottom).offset(12)
            make.horizontalEdges.equalToSuperview().inset(20)
        }
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
}
```

## Child View Controllers

Use the full containment sequence:

```swift
addChild(child)
containerView.addSubview(child.view)
child.view.snp.makeConstraints { make in
    make.edges.equalToSuperview()
}
child.didMove(toParent: self)
```

Remove in reverse:

```swift
child.willMove(toParent: nil)
child.view.removeFromSuperview()
child.removeFromParent()
```

Skipping containment breaks appearance callbacks, trait propagation, safe-area
behavior, and SwiftUI environment propagation when the child is a hosting
controller.

## Checklist

- [ ] `viewDidLoad` contains one-time setup only.
- [ ] Geometry-dependent first update is in `viewIsAppearing`.
- [ ] Every lifecycle override calls `super`.
- [ ] Layout style matches the project: SnapKit or native Auto Layout.
- [ ] Constraints are created once and then updated/toggled.
- [ ] Child view controllers use the full containment sequence.
