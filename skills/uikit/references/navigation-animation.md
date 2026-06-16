# UIKit Navigation and Animation

Use this reference for navigation controllers, bar appearance, deep links,
transition safety, and UIKit animation API selection.

Official docs:

- `UINavigationController`: https://sosumi.ai/documentation/uikit/uinavigationcontroller
- `UINavigationBarAppearance`: https://sosumi.ai/documentation/uikit/uinavigationbarappearance
- `UIViewPropertyAnimator`: https://sosumi.ai/documentation/uikit/uiviewpropertyanimator

## Contents

- [Navigation Appearance](#navigation-appearance)
- [Stack Changes](#stack-changes)
- [Animation Choice](#animation-choice)
- [Constraint Animation](#constraint-animation)
- [Checklist](#checklist)

## Navigation Appearance

- Use `navigationItem` for per-screen appearance.
- Use `UINavigationBar.appearance()` only for app-wide design system defaults.
- Configure standard and scroll-edge appearances deliberately.
- Set `prefersLargeTitles` once at navigation-bar level; use
  `largeTitleDisplayMode` per view controller.

```swift
override func viewDidLoad() {
    super.viewDidLoad()

    let appearance = UINavigationBarAppearance()
    appearance.configureWithOpaqueBackground()
    appearance.backgroundColor = .systemBackground

    navigationItem.standardAppearance = appearance
    navigationItem.scrollEdgeAppearance = appearance
    navigationItem.compactAppearance = appearance
}
```

## Stack Changes

For deep links, replace the stack directly:

```swift
navigationController?.setViewControllers([
    HomeController(),
    ProfileController(userID: id)
], animated: false)
```

Before pushing/popping from callbacks, guard transition state:

```swift
guard navigationController?.transitionCoordinator == nil else { return }
navigationController?.pushViewController(detail, animated: true)
```

## Animation Choice

| API | Use for |
| --- | --- |
| `UIView.animate` | Simple one-shot view property and layout animations |
| `UIViewPropertyAnimator` | Interactive, interruptible, gesture-driven animations |
| Core Animation | Layer-only properties such as shadow, transform, stroke, path |

For Core Animation, set the model layer value before adding the animation.

## Constraint Animation

```swift
view.layoutIfNeeded()
panel.snp.updateConstraints { make in
    make.height.equalTo(240)
}
UIView.animate(withDuration: 0.25) {
    self.view.layoutIfNeeded()
}
```

Call `layoutIfNeeded()` on the nearest common superview that owns the affected
constraints.

## Checklist

- [ ] Appearance is configured in `viewDidLoad` or a design-system setup path.
- [ ] Per-screen appearance uses `navigationItem`, not global mutation.
- [ ] Deep links use `setViewControllers`.
- [ ] Push/pop calls are guarded against concurrent transitions.
- [ ] Animation API matches the interaction model.
- [ ] Constraint animations update constants before animating layout.
- [ ] Core Animation updates the model layer value before adding animation.
