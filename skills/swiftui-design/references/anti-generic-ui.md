# Anti-Generic SwiftUI UI

Use this reference when a UI looks generic, AI-generated, template-like, or disconnected from the product.

## Patterns To Avoid

| Pattern | Why It Fails | Use Instead |
| --- | --- | --- |
| Purple-blue gradient background | Overused default that rarely matches brand or task | Brand-specific accent on neutral surfaces |
| Emoji as icons | Inconsistent rendering and poor styling control | SF Symbols or real icon assets |
| Rounded card with a colored left stripe | Common template card with weak hierarchy | Better typography, spacing, icon/state treatment |
| Centered "Welcome to App" hero | Wastes first screen in an app workflow | Real content, next action, current state |
| Default blue for every interactive element | Looks uncustomized | Product accent via semantic token and `.tint(...)` |
| Symmetric three-column feature grid | SaaS landing-page habit, weak native app fit | Content-driven lists, adaptive grids, asymmetric feature blocks |
| Neon-on-dark dashboard | Often low contrast and visually cliched | Native dark mode neutrals with restrained semantic color |
| Stock-like SVG illustration | Feels disconnected from the product | Real photography, brand assets, SF Symbols, or clean placeholders |
| One-card-per-section page | Makes hierarchy flat and heavy | Full-width sections, grouped lists, toolbars, sheets, split views |

These are not absolute bans for every product. If a brand truly owns one of these patterns, use it deliberately and document why it fits.

## Replacement Heuristics

- Replace decorative gradients with meaningful depth: material, grouped backgrounds, subtle borders, image treatments, or state color.
- Replace generic feature grids with actual product objects: recent files, active connection, health metrics, transactions, workouts, tasks, devices, chats, or messages.
- Replace a big hero with the first useful state: current status, next task, saved item, recommendation, or primary control.
- Replace random icon decoration with one consistent symbol style: outline for inactive, fill for active, matching weight with adjacent text.
- Replace invented slogans with concrete labels and data from the app model.

## SwiftUI Examples

Prefer SF Symbols for functional controls:

```swift
Label("Connect", systemImage: "lock.shield")
    .font(.headline)
```

Apply a product accent once near the root:

```swift
RootView()
    .tint(DesignTokens.accent)
```

Show content before explanation:

```swift
VStack(alignment: .leading, spacing: DesignTokens.spacing24) {
    ConnectionStatusCard(status: model.status)
    RecentLocationsSection(locations: model.recentLocations)
    SecurityActions(actions: model.availableActions)
}
```

## Self-Review Questions

- Would this screen still make sense if all decorative elements were removed?
- Can the user tell what to do next without reading marketing copy?
- Does the layout reflect real app content, or could it belong to any app?
- Are tokens semantic and reused, or are colors and spacing invented per view?
- Is there one memorable product-specific detail, not many decorative flourishes?
