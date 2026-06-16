---
name: uikit
description: Build, review, debug, or modernize UIKit code in Swift apps. Use when working with UIViewController lifecycle, custom UIView screens, Auto Layout, SnapKit, UICollectionViewDiffableDataSource, compositional layouts, UITableView or UICollectionView cells, UIContentConfiguration, UINavigationController, UINavigationBarAppearance, UIView animations, UIViewPropertyAnimator, memory leaks, Task cancellation, @MainActor UI updates, image loading, keyboard handling, Dynamic Type, Dark Mode, accessibility, trait changes, or UIKit-SwiftUI interoperability.
---

# UIKit

Use this skill for production UIKit work: view controllers, views, layout,
collection/list screens, cells, navigation, animations, memory, concurrency,
keyboard handling, images, adaptive appearance, accessibility, and SwiftUI
interop.

This is not an architecture skill. Use `ios-architecture` for MVC, MVVM, TCA,
Clean Architecture, Coordinator, dependency direction, and module boundaries.
Use this skill when UIKit code needs to be correct, modern, performant, and
maintainable regardless of architecture.

## Contents

- [Workflow](#workflow)
- [Reference Loading](#reference-loading)
- [Core Rules](#core-rules)
- [Review Checklist](#review-checklist)
- [Common Mistakes](#common-mistakes)
- [References](#references)

## Workflow

1. Classify the work: lifecycle/layout, collection/list, navigation/animation,
   memory/concurrency, images/keyboard, adaptive/accessibility, or SwiftUI
   interop.
2. Load the minimum matching reference from [Reference Loading](#reference-loading).
3. Preserve the project's layout style. Use SnapKit if the app uses SnapKit;
   use native Auto Layout if that is the local convention.
4. Prefer modern UIKit APIs when they reduce crashes or boilerplate: diffable
   data sources, compositional layout, cell registrations, content
   configurations, keyboard layout guide, and trait registration.
5. Review lifecycle and ownership before polishing code style. UIKit bugs are
   usually lifecycle, identity, layout, cancellation, or retain-cycle bugs.

## Reference Loading

| If the task involves | Load |
| --- | --- |
| `UIViewController`, custom `UIView`, Auto Layout, SnapKit, layout lifecycle | [lifecycle-layout.md](references/lifecycle-layout.md) |
| `UICollectionView`, `UITableView`, diffable data source, cells, list performance | [collections-lists.md](references/collections-lists.md) |
| Navigation bars, push/pop, deep links, transitions, animations | [navigation-animation.md](references/navigation-animation.md) |
| Retain cycles, delegates, timers, `Task`, `@MainActor`, cancellation | [memory-concurrency.md](references/memory-concurrency.md) |
| Async image loading, downsampling, keyboard avoidance, scroll views | [images-keyboard.md](references/images-keyboard.md) |
| Dynamic Type, Dark Mode, traits, VoiceOver, accessibility actions | [adaptive-accessibility.md](references/adaptive-accessibility.md) |
| `UIHostingController`, `UIViewRepresentable`, `UIHostingConfiguration` | [swiftui-interop.md](references/swiftui-interop.md) |
| Modernizing legacy UIKit or reviewing broad UIKit code | Load all matching references, then apply the [Review Checklist](#review-checklist) |

## Core Rules

- Use `viewDidLoad` for one-time setup only: subviews, constraints, delegates,
  data source construction, registrations.
- Use `viewIsAppearing(_:)` for geometry/trait-dependent first-appearance work
  such as scroll positioning, current trait configuration, and layout-dependent
  updates.
- Keep layout in views, cells, and reusable components. Controllers may install
  the root view and coordinate events, but should not own every constraint.
- Build constraints once. Update constants or toggle prepared constraints
  instead of removing/recreating constraints on every state change.
- With SnapKit, use `makeConstraints` for initial setup, `updateConstraints`
  for constants, and `remakeConstraints` only for a deliberate layout shape
  change.
- Use stable identifiers for diffable data sources. Do not use large mutable
  model structs as item identity.
- Prefer `UICollectionView.CellRegistration` and content/background
  configurations over string reuse identifiers and deprecated cell properties.
- Set navigation bar appearance per view controller through `navigationItem`
  unless the app intentionally uses global appearance.
- Store and cancel async `Task`s tied to a screen lifecycle. Check cancellation
  before applying UI updates after `await`.
- Use `[weak self]` in escaping closures by default. Delegates should be weak
  and class-constrained.
- Use `UIKeyboardLayoutGuide` for keyboard avoidance when available instead of
  manual keyboard frame math.
- Downsample large images to display size before assigning them to image views.
- Treat custom `UIView` subclasses as inaccessible until labels, traits,
  actions, and Dynamic Type behavior are explicitly reviewed.

## Review Checklist

- [ ] Lifecycle methods are used for their intended purpose and call `super`.
- [ ] Programmatic layout follows the project style: SnapKit or native Auto
      Layout, not a mixed one-off style.
- [ ] Constraints are created once and updated predictably.
- [ ] Collection/list screens use stable identity and avoid unnecessary full
      reloads.
- [ ] Cells reset reusable state, cancel async work, and use content
      configurations where appropriate.
- [ ] Navigation appearance is configured in the correct scope and transitions
      are not started concurrently.
- [ ] Animations update the model value and handle cancellation/completion.
- [ ] Timers, notifications, delegates, closures, and tasks do not retain view
      controllers after dismissal.
- [ ] UI updates happen on the main actor.
- [ ] Image loading avoids full-size bitmap memory spikes and cell reuse races.
- [ ] Keyboard avoidance works with hardware, floating, split, and software
      keyboards where relevant.
- [ ] Dynamic Type, Dark Mode, trait changes, and VoiceOver are supported.
- [ ] UIKit-SwiftUI bridges use proper containment, sizing, and cleanup.

## Common Mistakes

- Doing geometry work in `viewDidLoad`.
- Recreating constraints during every update instead of changing constants.
- Using `reloadData()` or full snapshot reloads for small content changes.
- Using unstable values as diffable item identifiers.
- Setting navigation bar appearance directly on `navigationController` from
  `viewWillAppear` for one screen.
- Starting another push/pop while a transition is already active.
- Capturing `self` strongly in cell callbacks, timers, notifications, or stored
  closures.
- Letting async image tasks finish into reused cells.
- Loading full-resolution photos just to show thumbnails.
- Manually calculating keyboard frames when a layout guide would express the
  constraint.
- Assigning `accessibilityTraits` wholesale and overwriting UIKit defaults.
- Embedding `UIHostingController` without full child view-controller
  containment.

## References

- [lifecycle-layout.md](references/lifecycle-layout.md) - View lifecycle, custom views, Auto Layout, SnapKit, child containment.
- [collections-lists.md](references/collections-lists.md) - Diffable data sources, compositional layout, cells, reuse, performance.
- [navigation-animation.md](references/navigation-animation.md) - Navigation appearance, deep links, transition safety, animation API choice.
- [memory-concurrency.md](references/memory-concurrency.md) - Retain cycles, delegate ownership, timers, tasks, main actor boundaries.
- [images-keyboard.md](references/images-keyboard.md) - Image downsampling, async cell loading, keyboard layout guide, scroll behavior.
- [adaptive-accessibility.md](references/adaptive-accessibility.md) - Traits, Dynamic Type, Dark Mode, accessibility labels/actions.
- [swiftui-interop.md](references/swiftui-interop.md) - Hosting controllers, representables, hosting configuration, cleanup.
