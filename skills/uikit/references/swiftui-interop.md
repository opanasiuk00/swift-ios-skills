# UIKit and SwiftUI Interoperability

Use this reference when embedding SwiftUI in UIKit, wrapping UIKit for SwiftUI,
or using SwiftUI content inside UIKit cells.

Official docs:

- `UIHostingController`: https://sosumi.ai/documentation/swiftui/uihostingcontroller
- `UIViewRepresentable`: https://sosumi.ai/documentation/swiftui/uiviewrepresentable
- `UIViewControllerRepresentable`: https://sosumi.ai/documentation/swiftui/uiviewcontrollerrepresentable

## Contents

- [Hosting Controllers](#hosting-controllers)
- [Representables](#representables)
- [SwiftUI in Cells](#swiftui-in-cells)
- [State and Cleanup](#state-and-cleanup)
- [Checklist](#checklist)

## Hosting Controllers

Embed `UIHostingController` using full child containment and retain it:

```swift
final class ParentController: UIViewController {
    private let hostingController = UIHostingController(rootView: SummaryView())

    override func viewDidLoad() {
        super.viewDidLoad()

        addChild(hostingController)
        view.addSubview(hostingController.view)
        hostingController.view.snp.makeConstraints { make in
            make.edges.equalToSuperview()
        }
        hostingController.didMove(toParent: self)
    }
}
```

Do not create a hosting controller as a local variable and only keep its view.

## Representables

`UIViewRepresentable` lifecycle:

1. `makeCoordinator()`
2. `makeUIView(context:)`
3. `updateUIView(_:context:)`
4. `dismantleUIView(_:coordinator:)`

Create the UIKit view once in `makeUIView`. Put state-dependent updates in
`updateUIView` with equality guards:

```swift
func updateUIView(_ textField: UITextField, context: Context) {
    if textField.text != text {
        textField.text = text
    }
}
```

Do not push or present view controllers from `updateUIViewController`; it runs
for state updates, not only user intent.

## SwiftUI in Cells

Prefer `UIHostingConfiguration` for simple SwiftUI cell content:

```swift
cell.contentConfiguration = UIHostingConfiguration {
    UserRow(user: user)
}
```

Use manual `UIHostingController` cell containment only when the cell needs
controller-level behavior that `UIHostingConfiguration` cannot provide.

## State and Cleanup

Use coordinators for delegates and target/action bridges. Avoid feedback loops:

- SwiftUI state changes update UIKit in `updateUIView`.
- UIKit delegate callbacks update bindings only when the value actually changed.
- Cleanup observers, timers, and delegates in `dismantleUIView` or
  `dismantleUIViewController`.

## Checklist

- [ ] `UIHostingController` is retained as a property.
- [ ] Hosting controllers use full child containment.
- [ ] Sizing is explicit for Auto Layout or cell contexts.
- [ ] Representables create views once and update mutable state in update calls.
- [ ] Update methods guard against feedback loops.
- [ ] Navigation/presentation does not happen from unguarded update methods.
- [ ] Dismantle methods remove observers, timers, delegates, and tasks.
