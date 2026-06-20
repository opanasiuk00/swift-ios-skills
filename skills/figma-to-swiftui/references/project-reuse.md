# Project Reuse Pass for Figma to SwiftUI

Run this pass before writing SwiftUI or adding assets/tokens. The goal is to preserve the target project's design system instead of creating parallel colors, images, components, or layout conventions.

## Contents

- [1. Discover Existing Systems](#1-discover-existing-systems)
- [2. Reuse Decision Rules](#2-reuse-decision-rules)
- [3. Colors and Tokens](#3-colors-and-tokens)
- [4. Images and Asset Catalogs](#4-images-and-asset-catalogs)
- [5. SwiftUI Components](#5-swiftui-components)
- [6. Layout and Pattern Review](#6-layout-and-pattern-review)
- [7. Checklist](#7-checklist)

## 1. Discover Existing Systems

Search the target project before implementation:

```bash
rg -n "extension Color|enum .*Color|struct .*Theme|Color\\(\"|\\.foregroundStyle|\\.background" .
rg --files | rg "Assets\\.xcassets|\\.colorset|\\.imageset|Generated|R\\.swift|SwiftGen"
rg -n "struct .*: View|struct .*ButtonStyle|struct .*ViewModifier|enum .*Style|enum .*Variant" .
rg -n "Font\\.|font\\(|fontWidth|tracking|lineSpacing|Spacing|Radius|Corner|Shadow" .
```

Also inspect adjacent screens in the same feature/module. Adjacent code often reveals the real project naming, layout, localization, and dependency patterns faster than global search.

## 2. Reuse Decision Rules

Use existing project items when any of these are true:

- Same color value already exists in Asset Catalog, a `Color` extension, theme enum, or design-system module.
- Same image/logo/icon/source node is already present in an `.imageset`.
- Same visual component already exists as a `View`, `ButtonStyle`, `ToggleStyle`, `ViewModifier`, or design-system component.
- Same typography/spacing/radius/shadow token already exists, even if Figma uses a different token name.
- Code Connect maps the Figma component to a project component.

Add a new item only when it is genuinely missing. Add it where the project already stores that item type, with the same naming style and module boundary.

Do not create a new `Color+Figma.swift`, `FigmaAssets`, `FigmaSpacing`, or one-off design-system clone unless the project already has that exact convention.

## 3. Colors and Tokens

Match colors by exact resolved value first, then by semantic role:

1. Resolve Figma variable modes and raw hex/opacity.
2. Search project color assets and token code for the same value.
3. If exact value exists, use the existing project name even when Figma's variable name differs.
4. If no exact value exists but an adjacent screen uses a semantic token for the same role, prefer that token when it is visually acceptable for the project.
5. If the color is new, add it to the existing color system: `.colorset`, theme enum, token extension, or design-system package according to project convention.

For opacity, preserve whether Figma used fill opacity or layer opacity. Do not convert a semi-transparent color token into a whole-view `.opacity()` unless the Figma layer opacity applies to all children.

For typography, spacing, radius, and shadow, follow the same rule: reuse existing token/helper if it represents the same value or role; add new tokens in the existing token location only when missing.

## 4. Images and Asset Catalogs

Before exporting from Figma:

1. Search asset catalogs by likely semantic names, layer names, and feature names.
2. Inspect generated asset helpers if the project uses SwiftGen, R.swift, or custom asset enums.
3. Reuse the existing asset if it is the same source graphic or visually identical shipped artwork.
4. Export from Figma only when the image/icon/logo/illustration is missing.

When adding a new asset:

- Put it in the same asset catalog used by the feature or design system.
- Follow the existing naming convention and bundle/module access pattern.
- Add `@1x`, `@2x`, `@3x`, and `Contents.json` only if the project uses explicit scaled PNGs.
- Use the project's typed asset access if one exists. Do not bypass generated asset APIs with raw string names unless the project already does that.

For Figma icons, do not replace with SF Symbols unless the user approves. For system chrome, prefer native iOS behavior instead of bundled Figma assets.

## 5. SwiftUI Components

Before creating a new component:

1. Check Code Connect mappings for the Figma node.
2. Search the project for visually similar `View` structs, styles, modifiers, and design-system components.
3. Inspect call sites to understand accepted parameters, state handling, localization, and accessibility.
4. Reuse the component if its public API can express the Figma variant without distorting its intended use.
5. Extend the existing component only when the new variant belongs to the same design-system concept.
6. Create a new component only when no existing component fits or extending one would make it ambiguous.

When a Figma component has variants, map them to existing project enums or style parameters first. If the project already has `variant`, `style`, `size`, `state`, or `kind` enums, use those names instead of creating Figma-named duplicates.

## 6. Layout and Pattern Review

After drafting SwiftUI, review the code with the relevant sibling skills:

- Apply `swiftui-layout-components` for stack/grid/list/scroll/form/control selection, fixed vs flexible sizing, safe areas, overlays, and layout pitfalls.
- Apply `swiftui-patterns` for state ownership, view decomposition, helper extraction, environment usage, async work, and final SwiftUI structure.

This review should change code when it finds a real mismatch with project conventions or SwiftUI behavior. Do not rewrite correct project-specific code just to fit a generic example.

## 7. Checklist

- Existing color/token system was found or intentionally absent.
- Every Figma color was mapped to an existing token or added in the existing token location.
- Existing assets were searched before Figma export.
- New assets, if any, were added to the correct catalog with project naming and access style.
- Code Connect and existing SwiftUI components were checked before creating new components.
- Reused components keep their existing API and semantics.
- New variants were added to existing style enums when that matched project design-system ownership.
- `swiftui-layout-components` and `swiftui-patterns` were applied before finalizing.
