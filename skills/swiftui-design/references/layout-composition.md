# SwiftUI Layout Composition

Use this reference when building or improving a complete SwiftUI screen.

## Screen Structure

Start with the user task, then arrange content by priority:

```swift
struct DashboardView: View {
    var body: some View {
        ScrollView {
            VStack(alignment: .leading, spacing: DesignTokens.Spacing.lg) {
                HeaderSection()
                PrimaryStatusSection()
                SecondaryContentSection()
                RecentActivitySection()
            }
            .padding(.horizontal, DesignTokens.Spacing.md)
            .padding(.vertical, DesignTokens.Spacing.lg)
        }
        .background(DesignTokens.Color.groupedBackground)
    }
}
```

Rules:

- Use real content sections instead of a decorative welcome block.
- Prefer semantic section views over one large anonymous `VStack`.
- Use `frame(maxWidth: .infinity, alignment: .leading)` for flexible rows and cards.
- Avoid `GeometryReader` for routine sizing. Prefer adaptive stacks, `ViewThatFits`, `containerRelativeFrame`, grid items, size classes, and `Layout` when appropriate.

## Cards and Surfaces

Cards work best for repeated items, summaries, and grouped controls. Do not make every page section a card.

```swift
struct SummaryCard<Content: View>: View {
    @ViewBuilder var content: Content

    var body: some View {
        content
            .padding(DesignTokens.Spacing.md)
            .frame(maxWidth: .infinity, alignment: .leading)
            .background(DesignTokens.Color.surface)
            .clipShape(RoundedRectangle(cornerRadius: DesignTokens.Radius.md, style: .continuous))
    }
}
```

Card checks:

- Clear internal hierarchy.
- Consistent padding and radius.
- No nested cards.
- Shadow or border is subtle and used consistently.

## Lists

Use `List` for platform-native long lists and editing behavior. Use `LazyVStack` for custom short-to-medium feeds.

```swift
LazyVStack(spacing: 0) {
    ForEach(items) { item in
        ItemRow(item: item)
        if item.id != items.last?.id {
            Divider().padding(.leading, DesignTokens.Spacing.md)
        }
    }
}
.background(DesignTokens.Color.surface)
.clipShape(RoundedRectangle(cornerRadius: DesignTokens.Radius.md, style: .continuous))
```

## Grids

Prefer adaptive grids over fixed column counts:

```swift
let columns = [
    GridItem(.adaptive(minimum: 160), spacing: DesignTokens.Spacing.md)
]

LazyVGrid(columns: columns, spacing: DesignTokens.Spacing.md) {
    ForEach(items) { item in
        TileView(item: item)
    }
}
```

Avoid feature grids that exist only to fill space. Grid content should be real product objects.

## Empty, Loading, and Error States

Use native patterns where they fit:

```swift
ContentUnavailableView {
    Label("No Saved Locations", systemImage: "mappin.slash")
} description: {
    Text("Add a location to connect faster next time.")
} actions: {
    Button("Add Location") {
        addLocation()
    }
}
```

Loading:

```swift
VStack(spacing: DesignTokens.Spacing.md) {
    ProgressView()
    Text("Loading")
        .font(.caption)
        .foregroundStyle(.secondary)
}
.frame(maxWidth: .infinity, maxHeight: .infinity)
```

For content skeletons, prefer `.redacted(reason: .placeholder)` over a blank screen.

## iPad and macOS Adaptation

Do not simply stretch phone layouts.

- Use `NavigationSplitView` for master-detail flows.
- Use sidebars, inspectors, columns, and persistent toolbars when they reduce navigation friction.
- Increase information density before increasing decorative scale.
- Use `horizontalSizeClass`, `containerRelativeFrame`, adaptive grids, and `ViewThatFits` to reflow content.

## Composition Checklist

- Primary content appears before secondary decoration.
- Header height is proportional to the task and does not bury content.
- Layout works with long localized strings.
- Scrollable regions are obvious and do not trap controls.
- Components have stable dimensions through loading, empty, selected, and error states.
- iPad/macOS layout uses extra space for workflow efficiency.
