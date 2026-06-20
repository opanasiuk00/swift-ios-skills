---
name: figma-to-swiftui
description: Convert Figma design URLs, selected nodes, frames, components, source briefs, multi-screen flows, or Dev Mode handoffs into production SwiftUI for iOS, iPadOS, macOS, watchOS, or visionOS. Use for Figma MCP design-to-code work, design context fetching, screenshot comparison, Figma variables to SwiftUI tokens, asset export into Xcode asset catalogs, component variant translation, Code Connect reuse, flow and navigation inference between Figma screens, or adapting existing SwiftUI screens to match Figma designs. Do not use for web, React, or generic visual design without a Figma source.
---

# Figma to SwiftUI

Use this skill to turn Figma handoff material into native SwiftUI that follows the target project's existing architecture, design system, dependencies, and platform conventions.

This skill handles visual translation and implementation workflow. It does not own app architecture decisions; use `ios-architecture`, `swiftui-patterns`, `swiftui-navigation`, or `swiftui-layout-components` when those boundaries matter.

## Contents

- [Workflow](#workflow)
- [Reference Loading](#reference-loading)
- [MCP Rules](#mcp-rules)
- [Implementation Rules](#implementation-rules)
- [Common Mistakes](#common-mistakes)
- [Review Checklist](#review-checklist)
- [References](#references)

## Workflow

1. Read any source brief, ticket, `.md`, `.txt`, or inline product spec before Figma calls. Extract scope, screens, actions, async work, states, constraints, and out-of-scope items.
2. Parse the Figma URL. Extract `fileKey` from `/design/:fileKey/...` or legacy `/file/:fileKey/...`; extract `node-id` and convert URL form `12-34` to MCP form `12:34`.
3. Reject prototype or FigJam URLs for SwiftUI implementation. Ask for a `/design/` or `/file/` node-specific URL.
4. If the target node may be a page, root, flow, multi-screen frame, or ambiguous container, run metadata-based screen discovery before fetching full design context.
5. Fetch design context for the exact screen/component node, then capture a screenshot. Treat the screenshot as the visual truth and design context as the structured spec.
6. When the user provides multiple screens, a frame group, or a flow, build a screen/interaction map before coding. Identify each screen's role, primary actions, back/skip/close actions, and likely destinations; use Figma prototype links when available and infer from names/copy/layout only when links are absent.
7. Run the project reuse pass before coding. Inventory existing colors, asset catalogs, image wrappers, typography, spacing, reusable SwiftUI components, modifiers, and Code Connect mappings.
8. Fetch Figma variables once per file when tokens matter. Map by exact value first, then semantic name. If the project already has the same color/token/asset/component, use it; if not, add the new item in the project's existing location and naming style.
9. Build an asset inventory before coding. Reuse existing asset catalog images when they match; download Figma-owned icons, logos, illustrations, and static image fills only when missing. Do not substitute with SF Symbols unless the user approves.
10. Check Code Connect mappings and existing project components before building a new component.
11. Inspect the target Xcode project for existing patterns, dependencies, asset naming, localization, image loading, animations, design tokens, navigation/router style, and deployment target.
12. Implement native SwiftUI from the design properties. Do not port React, Tailwind, HTML, CSS, or MCP sample code.
13. For existing-screen updates, perform an adaptation audit before edits: list ADD, UPDATE, REMOVE differences with exact old-to-new values.
14. Before finalizing SwiftUI code, apply `swiftui-layout-components` for layout/container correctness, `swiftui-patterns` for view decomposition/state ownership/project-style composition, and `swiftui-navigation` for push/sheet/tab/router correctness when screens connect.
15. Validate only when the user asks or the task explicitly includes validation. Use screenshot comparison, simulator, previews, or snapshot tests according to the user's choice.
16. Register Code Connect mappings after creating stable reusable components that correspond to Figma components.

## Reference Loading

Load only the reference needed for the current step:

| Need | Read |
| --- | --- |
| Brief, ticket, source doc, scope extraction | `references/source-document.md` |
| Ambiguous root/page/multi-screen node | `references/screen-discovery.md` |
| Large Figma nodes, timeouts, section splitting | `references/fetch-strategy.md` |
| MCP connection behavior or troubleshooting | `references/figma-mcp-setup.md` |
| Multiple screens, login/onboarding/auth flows, button-to-screen transitions, and navigation inference | `references/multi-screen-flow.md` |
| Exact visual matching and screenshot cross-check | `references/visual-fidelity.md` |
| Auto Layout, padding, sizing, effects, animation mapping | `references/layout-translation.md` |
| iPhone/iPad/macOS adaptive layout | `references/responsive-layout.md` |
| Existing colors, assets, typography, components, and project reuse before adding new code | `references/project-reuse.md` |
| Figma variables to SwiftUI tokens | `references/design-token-mapping.md` |
| Figma component variants to SwiftUI enums/styles | `references/component-variants.md` |
| Icons, logos, PNG export, asset catalog work | `references/asset-handling.md` |
| Updating an existing SwiftUI screen from Figma | `references/adaptation-workflow.md` |

## MCP Rules

- Always target a concrete node. If the URL lacks `node-id`, ask for a node-specific URL or use the selected node in a Figma desktop MCP flow.
- Use `get_metadata` before `get_design_context` for root, page, flow, large, or ambiguous nodes.
- Use `get_design_context` for structured layout, typography, color, asset hints, and component hierarchy.
- Use `get_screenshot` for the visual reference and for Figma-rendered asset exports when needed.
- Use `get_variable_defs` once per Figma file when variables or token mapping are relevant.
- Use Code Connect lookup before creating reusable components; use existing mapped code when available.
- If context is truncated or times out, do not retry the same node blindly. Fetch metadata, split into meaningful child nodes, and continue section by section.

## Implementation Rules

- Project conventions win over generic output. Reuse existing SwiftUI components, asset catalog colors, typography helpers, image loaders, localization patterns, and animation libraries.
- Figma output is a spec carrier. Convert layout, colors, typography, effects, and assets into SwiftUI; do not translate React/Tailwind syntax directly.
- Reuse before creating. Search the target project for matching colors, image assets, typography helpers, spacing/radius/shadow tokens, `View` structs, `ButtonStyle`s, `ViewModifier`s, and Code Connect mappings before introducing any new file, token, asset, or component.
- Add missing design-system items where the project already stores that kind of item. Do not create a parallel color extension, asset namespace, token enum, or component style just for the Figma screen.
- Multi-screen Figma input is a flow specification, not a pile of independent screens. Map screen roles and actions before implementation, then use the target project's existing navigation/router pattern.
- Preserve platform behavior. Do not implement mockup-only system chrome such as status bar, home indicator, keyboard, native back button, system alerts, or native share sheet.
- Prefer native SwiftUI controls when they match the design. Use custom controls only when Figma requires a materially different structure or state.
- Every visible Figma-owned image, logo, icon, and illustration must be represented by a real asset or approved remote source.
- Every custom number in code should trace to a token, Figma value, project convention, or explicit implementation note.
- Check deployment target before using APIs such as `NavigationStack`, `Grid`, `containerRelativeFrame`, `scrollTargetBehavior`, `onScrollGeometryChange`, or `glassEffect`.
- Account for accessibility, Dynamic Type, dark mode, localization, safe areas, loading, empty, error, disabled, pressed, selected, and long-content states.

## Common Mistakes

| Mistake | Better Approach |
| --- | --- |
| Fetching a whole Figma page with `get_design_context` | Run `get_metadata`, choose the exact screen/component node |
| Implementing from the MCP code sample | Extract design properties and build native SwiftUI |
| Replacing a Figma logo/icon with an SF Symbol | Export the Figma asset or ask for approval |
| Drawing status bars, keyboards, or home indicators | Let iOS provide system UI |
| Ignoring existing project tokens and components | Map Figma values to project design system first |
| Treating iPhone frame width as fixed SwiftUI width | Use flexible frames, adaptive layout, or size classes |
| Skipping line height, letter spacing, shadows, or borders | Carry all specified visual properties |
| Updating existing screens without a diff checklist | Run the adaptation audit first |
| Adding a new color/image/component that already exists | Run the project reuse pass and use the project's existing token, asset, or component |
| Treating Figma variables as new app tokens by default | Match by exact value and existing semantic use before adding tokens |
| Building custom layout without SwiftUI skill review | Apply `swiftui-layout-components` and `swiftui-patterns` before finalizing |
| Implementing several supplied screens as disconnected views | Build a flow map, infer actions/destinations, then apply `swiftui-navigation` and the project router pattern |
| Guessing login/signup/onboarding transitions from button text without checking Figma links or project routes | Prefer prototype links and existing route names; mark uncertain edges before coding |

## Review Checklist

- Source brief, if present, was read before Figma calls.
- The target Figma node is unambiguous and scoped correctly.
- Design context and screenshot were both fetched for each implemented screen/component.
- Multi-screen input has a screen/interaction map with roles, primary actions, and destinations.
- The project reuse pass was completed before coding or asset additions.
- Tokens and components were mapped to existing project systems where possible.
- Asset inventory covers every visible non-text Figma-owned element.
- Existing asset catalog entries were reused when they matched the Figma visual/source.
- Existing SwiftUI components/styles/modifiers were reused when they already represented the Figma component.
- SwiftUI code does not port React/Tailwind directly.
- `swiftui-layout-components` and `swiftui-patterns` were applied to the final SwiftUI structure.
- `swiftui-navigation` was applied when implemented screens transition between each other.
- System chrome from mockups was skipped.
- Existing screen adaptations have ADD, UPDATE, REMOVE differences covered.
- API choices match the project's deployment target.
- Validation method is either user-approved or intentionally skipped per request.

## References

- `references/source-document.md`
- `references/screen-discovery.md`
- `references/fetch-strategy.md`
- `references/figma-mcp-setup.md`
- `references/multi-screen-flow.md`
- `references/visual-fidelity.md`
- `references/layout-translation.md`
- `references/responsive-layout.md`
- `references/project-reuse.md`
- `references/design-token-mapping.md`
- `references/component-variants.md`
- `references/asset-handling.md`
- `references/adaptation-workflow.md`
