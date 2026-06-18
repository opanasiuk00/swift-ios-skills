# SwiftUI Design Review

Use this reference for visual QA of SwiftUI screens from screenshots, Figma, or code.

## Review Process

1. Inspect the screen at realistic sizes: small iPhone, large iPhone, iPad or macOS when relevant.
2. Check light and dark mode.
3. Increase Dynamic Type and verify text still fits.
4. Review all visible states: loading, empty, error, disabled, selected, pressed, long content.
5. Score each dimension below from 1 to 10.
6. Fix anything below 7 before treating the design as ready.

## Five Dimensions

| Dimension | What To Check |
| --- | --- |
| Direction | The screen follows one coherent visual philosophy and fits the product category |
| Hierarchy | The user can identify primary content, primary action, and secondary information immediately |
| Craft | Spacing, alignment, typography, icon weight, radius, color, and media ratios are consistent |
| Function | The design makes the workflow easier, handles states, and keeps controls reachable |
| Originality | The screen has product-specific identity and avoids generic template patterns |

## Scoring Guide

| Score | Meaning |
| --- | --- |
| 1-3 | Redesign required; confusing, inaccessible, or obviously generic |
| 4-5 | Usable but template-like or inconsistent |
| 6-7 | Solid but needs polish in at least one dimension |
| 8-10 | Distinctive, coherent, accessible, and ready to ship |

## Review Template

```md
## Design Review: [Screen]

| Dimension | Score | Notes |
| --- | --- | --- |
| Direction | ?/10 | |
| Hierarchy | ?/10 | |
| Craft | ?/10 | |
| Function | ?/10 | |
| Originality | ?/10 | |

## Required Fixes
- [Issue] -> [Specific fix]

## Keep
- [Strong choice worth preserving]
```

## Common Fixes

- Weak hierarchy: increase contrast between title, section heading, body, metadata, and actions.
- Crowded layout: remove decorative panels, group related controls, and increase section spacing.
- Generic look: replace decorative gradient/hero/card patterns with product-specific content.
- Poor state coverage: add empty, loading, error, disabled, selected, and long-content variants.
- Inconsistent icons: align SF Symbol weight, fill state, and rendering mode.
- Accessibility risk: increase contrast, use text styles, keep 44 pt hit targets, and test large text.
