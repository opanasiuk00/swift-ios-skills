# Tokens, Typography, Color, and Spacing

Use this reference before implementing visual styling in SwiftUI.

## Token Model

Keep tokens semantic. Avoid names like `lightGray2` or `bigRadius`.

```swift
import SwiftUI

enum DesignTokens {
    enum Color {
        static let accent = SwiftUI.Color.accentColor
        static let background = SwiftUI.Color(.systemBackground)
        static let groupedBackground = SwiftUI.Color(.systemGroupedBackground)
        static let surface = SwiftUI.Color(.secondarySystemBackground)
        static let textPrimary = SwiftUI.Color.primary
        static let textSecondary = SwiftUI.Color.secondary
        static let divider = SwiftUI.Color(.separator)
        static let success = SwiftUI.Color.green
        static let warning = SwiftUI.Color.orange
        static let error = SwiftUI.Color.red
    }

    enum Spacing {
        static let xxs: CGFloat = 2
        static let xs: CGFloat = 4
        static let sm: CGFloat = 8
        static let md: CGFloat = 16
        static let lg: CGFloat = 24
        static let xl: CGFloat = 32
        static let xxl: CGFloat = 48
    }

    enum Radius {
        static let sm: CGFloat = 8
        static let md: CGFloat = 12
        static let lg: CGFloat = 16
    }
}
```

Use asset-catalog colors or custom adaptive colors when a brand requires exact hex values. Prefer system semantic colors when the product has no brand palette.

## Typography

Prefer SwiftUI text styles because they scale with Dynamic Type:

```swift
Text("Today")
    .font(.largeTitle.weight(.bold))

Text("Connection protected")
    .font(.headline)

Text("Last checked 2 min ago")
    .font(.caption)
    .foregroundStyle(.secondary)
```

Use custom sizes only when the design direction requires it, and keep them scaled:

```swift
struct StatusGlyph: View {
    @ScaledMetric(relativeTo: .title2) private var size = 28

    var body: some View {
        Image(systemName: "shield.checkered")
            .font(.system(size: size, weight: .semibold))
    }
}
```

For editorial or premium headings, use system serif instead of assuming a custom "New York" font file exists:

```swift
Text("Journal")
    .font(.system(.largeTitle, design: .serif).weight(.bold))
```

## Typography Rules

- Use at least three hierarchy levels on complex screens: title, section, body/caption.
- Keep body copy readable with native `.body`, `.callout`, or `.subheadline`.
- Avoid many custom font sizes on one screen.
- Do not use web-default font choices like Inter or Roboto unless the brand explicitly requires them and the font is bundled correctly.
- Check long text, localization expansion, and Dynamic Type before finalizing.

## Color Rules

- Use one dominant accent color, plus semantic status colors.
- Use `foregroundStyle(.primary)`, `.secondary`, and semantic tokens instead of hard-coded gray text.
- Set `.tint(...)` for controls at a high level.
- Avoid pure black and pure white as the only light/dark strategy; use system backgrounds or tested adaptive colors.
- Verify contrast for body text and important controls.
- Keep destructive, warning, success, and informational states visually distinct.

## SF Symbols

Use SF Symbols for native iconography:

```swift
Image(systemName: isSelected ? "heart.fill" : "heart")
    .symbolRenderingMode(.hierarchical)
    .foregroundStyle(isSelected ? DesignTokens.Color.accent : .secondary)
```

Guidelines:

- Match icon weight with adjacent text weight.
- Use fill variants for selected/active states.
- Keep icons in the same visual family within one component.
- Avoid decorative symbols that do not add meaning.

## Spacing and Shape

- Base most spacing on 4 or 8 pt steps.
- Phone horizontal padding usually starts at 16 pt; iPad and macOS can use wider gutters or columns.
- Keep minimum hit targets at 44 x 44 pt.
- Use stable dimensions for icon buttons, tiles, media, and grid cells so states do not shift layout.
- Keep corner radii consistent by component type.
