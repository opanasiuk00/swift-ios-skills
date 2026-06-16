# UIKit Adaptive Appearance and Accessibility

Use this reference for traits, Dynamic Type, Dark Mode, accessibility labels,
traits, actions, and custom views.

Official docs:

- `UITraitCollection`: https://sosumi.ai/documentation/uikit/uitraitcollection
- `UIAccessibility`: https://sosumi.ai/documentation/uikit/uiaccessibility
- Supporting Dark Mode: https://sosumi.ai/documentation/uikit/supporting-dark-mode-in-your-interface

## Contents

- [Trait Changes](#trait-changes)
- [Dynamic Type](#dynamic-type)
- [Dark Mode](#dark-mode)
- [Accessibility](#accessibility)
- [Checklist](#checklist)

## Trait Changes

Use targeted trait change registration when available:

```swift
registerForTraitChanges([UITraitHorizontalSizeClass.self]) {
    (self: Self, previousTraitCollection: UITraitCollection) in
    self.updateLayoutForCurrentTraits()
}
```

The handler is not an initial configuration callback. Do initial setup in
`viewIsAppearing(_:)` or the relevant setup path.

## Dynamic Type

```swift
label.font = .preferredFont(forTextStyle: .body)
label.adjustsFontForContentSizeCategory = true
label.numberOfLines = 0
```

If a custom font is required, use `UIFontMetrics` to scale it.

## Dark Mode

Prefer semantic colors:

```swift
view.backgroundColor = .systemBackground
titleLabel.textColor = .label
subtitleLabel.textColor = .secondaryLabel
```

Layer `CGColor` values do not automatically re-resolve after a trait change.
Reassign them from dynamic `UIColor` in a trait update path.

## Accessibility

For custom tappable views:

```swift
isAccessibilityElement = true
accessibilityLabel = title
accessibilityHint = "Opens details"
accessibilityTraits.insert(.button)
```

Modify traits by inserting/removing, not by replacing the full set unless you
intend to discard UIKit defaults.

For complex cell actions:

```swift
accessibilityCustomActions = [
    UIAccessibilityCustomAction(name: "Archive") { [weak self] _ in
        self?.archive()
        return true
    }
]
```

## Checklist

- [ ] Trait registration handles only relevant traits.
- [ ] Initial configuration does not rely on trait-change callbacks firing.
- [ ] Dynamic Type uses text styles or `UIFontMetrics`.
- [ ] Labels support multiple lines where text can grow.
- [ ] Semantic colors are used instead of hardcoded light/dark assumptions.
- [ ] Layer `CGColor` values are refreshed when traits change.
- [ ] Custom views set labels, hints, and traits.
- [ ] Accessibility traits are inserted/removed without wiping defaults.
- [ ] Complex cell actions are exposed through custom accessibility actions.
