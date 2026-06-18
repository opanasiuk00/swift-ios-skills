---
name: swiftui-design
description: Design, review, or improve SwiftUI visual interfaces for iOS, iPadOS, macOS, watchOS, or visionOS apps. Use when creating new SwiftUI screens, choosing a visual direction, avoiding generic AI-looking UI, defining design tokens, typography, color, spacing, layout rhythm, brand integration, empty/loading/error states, design polish, or performing a visual quality review of SwiftUI views.
---

# SwiftUI Design

Use this skill when a SwiftUI task has a visual product-design component: screen design, polish, brand fit, typography, color, spacing, layout rhythm, empty/loading/error states, or a review of whether the UI feels generic.

For state ownership, observation, and composition architecture, use `swiftui-patterns`. For NavigationStack, sheets, tabs, and deep links, use `swiftui-navigation`. For lists, grids, forms, scroll views, and component mechanics, use `swiftui-layout-components`.

## Contents

- [Workflow](#workflow)
- [Reference Loading](#reference-loading)
- [Core Rules](#core-rules)
- [Common Mistakes](#common-mistakes)
- [Review Checklist](#review-checklist)
- [References](#references)

## Workflow

1. Identify the product context before choosing visuals: app category, user job, platform, existing code style, screenshots, Figma, brand assets, and accessibility requirements.
2. If the request is vague, propose two or three distinct visual directions before coding. Do not present color swaps as separate directions.
3. Define semantic design tokens first: accent, background, surface, text, divider, success, warning, error, spacing, radius, and type scale.
4. Build the screen around real app content and task flow. App UIs should lead with usable content, not marketing hero filler.
5. Use SwiftUI-native primitives: `Color`, `Font.TextStyle`, `foregroundStyle`, `Image(systemName:)`, adaptive layout containers, semantic state views, Dynamic Type, and dark mode.
6. Add one restrained signature detail per important screen: a distinctive header, motion moment, layout choice, brand image treatment, or custom control state.
7. Review with screenshots when possible. Fix hierarchy, spacing, contrast, tap targets, state coverage, and generic visual patterns before calling the design done.

## Reference Loading

Load only the reference needed for the task:

| Need | Read |
| --- | --- |
| Vague prompt, brand direction, visual style options | `references/design-direction.md` |
| UI looks generic, AI-generated, or template-like | `references/anti-generic-ui.md` |
| Tokens, typography, color, spacing, Dynamic Type, dark mode | `references/tokens-typography-color.md` |
| Screen composition, cards, lists, grids, states, iPad adaptation | `references/layout-composition.md` |
| Screenshot/code review or final quality gate | `references/design-review.md` |

## Core Rules

- Prefer native Apple typography and controls unless the product has verified brand assets that require a custom direction.
- Use SF Symbols or real icon assets for functional icons. Do not use emoji as production icons.
- Use semantic colors and `foregroundStyle` for text and symbol styling. Avoid hard-coded random hex values scattered through views.
- Support Dynamic Type by starting from SwiftUI text styles where possible and using `@ScaledMetric` for size-dependent custom values.
- Use a 4/8 pt spacing system and stable dimensions for controls, cards, grids, and media. Avoid odd accidental padding values.
- Keep cards purposeful. Do not put cards inside cards, and do not turn every section into a floating panel.
- Avoid generic first-screen patterns: purple-blue gradients, centered welcome hero blocks, left-accent cards, three-column feature grids, stock-looking illustrations, and default blue tint everywhere.
- Use real product content, real brand media, or clean placeholders. Do not invent logos, brand palettes, or fake marketing claims.
- Design empty, loading, error, disabled, selected, pressed, and long-content states before shipping.
- Check contrast, 44 pt minimum hit targets, text wrapping, VoiceOver labels, reduce motion, and dark mode.

## Common Mistakes

| Mistake | Better Approach |
| --- | --- |
| Starting from decorative gradients | Start from task flow, content hierarchy, and brand tokens |
| Using emoji text as an icon | Use `Image(systemName:)` or a real asset |
| Random padding like 13, 17, 23 | Use a 4/8 pt spacing scale |
| Every action uses default blue | Define and apply a product accent with `.tint(...)` |
| Fixed text sizes everywhere | Prefer `Font.TextStyle`; use scaled metrics for custom sizes |
| Blank loading or empty states | Use `ProgressView`, redacted placeholders, or `ContentUnavailableView` |
| iPad layout is just stretched iPhone UI | Use extra space for split views, sidebars, columns, or richer content density |
| Visual review only in code | Review screenshots on phone and tablet sizes, light and dark mode |

## Review Checklist

- The screen has one clear visual direction and no conflicting style choices.
- The primary content and primary action are obvious within the first second.
- Typography has at least three clear levels and supports Dynamic Type.
- Spacing, corner radius, icon weight, image aspect ratios, and alignment are consistent.
- Colors are semantic, brand-appropriate, dark-mode aware, and accessible.
- Functional states are designed, not left as defaults or blank views.
- The result does not look like a generic SaaS/mobile template.
- Any Apple API claim has been checked against current official documentation when it affects implementation.

## References

- `references/design-direction.md`
- `references/anti-generic-ui.md`
- `references/tokens-typography-color.md`
- `references/layout-composition.md`
- `references/design-review.md`
