# SwiftUI Design Direction

Use this reference when the user asks for a new visual style, says "make it look better", provides only a rough idea, or wants brand polish.

## Direction Workflow

1. Clarify the product surface: consumer app, pro tool, media app, health app, finance app, onboarding, settings, dashboard, editor, or game companion.
2. Identify the user job: scan, compare, create, recover, decide, monitor, read, buy, learn, or configure.
3. Check existing visual context: app screenshots, Figma, asset catalog, color names, typography, icons, screenshots in the repo, and competitor references.
4. Propose two or three directions with different design philosophies.
5. Pick one direction, then define tokens and component rules before implementing screens.

## Useful Design Schools

| School | Best For | Visual Moves |
| --- | --- | --- |
| Informational | dashboards, finance, health, admin, monitoring | dense hierarchy, quiet surfaces, charts, compact metadata, strong alignment |
| Editorial | reading, travel, recipes, media, portfolios | serif display type, large imagery, generous margins, strong section rhythm |
| Expressive | creator tools, launches, playful consumer apps | bold accent, asymmetric composition, motion, custom empty states |
| Functional | utilities, VPN, security, settings, developer tools | restrained color, high scan speed, predictable controls, tight spacing |
| Warm Minimal | wellness, personal productivity, family, lifestyle | warm neutrals, soft surfaces, subtle texture, friendly but calm typography |

Do not treat these as themes. Use them as constraints for layout density, typography, color, and interaction choices.

## Direction Proposal Format

```md
## Direction A: Functional Control Room
- Best for: repeated daily use and fast scanning.
- Palette: warm neutral background, one clear accent, semantic status colors.
- Typography: system body, compact section headings, numeric emphasis where needed.
- Layout: dense lists, pinned controls, minimal decoration.
- Signature detail: active connection/status strip with subtle motion.

## Direction B: Editorial Product
- Best for: discovery, reading, learning, and product storytelling.
- Palette: neutral canvas, large media, restrained accent.
- Typography: serif display titles, system body.
- Layout: strong image/title rhythm, fewer cards, spacious reading blocks.
- Signature detail: photo-led header that collapses into navigation.
```

## Brand Asset Protocol

When the UI is for a real brand:

1. Ask for or locate real brand assets: logo, icon, colors, typography, screenshots, App Store page, website, and style guide.
2. Verify color and typography from official sources before using them as facts.
3. Prefer real logos and product images over generated illustrations.
4. If assets are missing, create neutral placeholders and mark them as placeholders in code comments or design notes.
5. Write a small brand spec before implementation.

## Minimal Brand Spec

```md
# Brand Spec

## Colors
- accent:
- accent pressed:
- background:
- surface:
- text primary:
- text secondary:
- divider:
- success:
- warning:
- error:

## Typography
- display:
- heading:
- body:
- caption:

## Spacing
- base grid:
- screen padding:
- section spacing:
- component spacing:

## Shape
- small radius:
- medium radius:
- large radius:

## Assets
- logo:
- icon style:
- image treatment:
```

## Direction Checks

- A vague prompt received at least two genuinely different options.
- The chosen direction matches the app category and user job.
- Visual decisions came from content and brand context, not decorative defaults.
- The direction can be implemented with SwiftUI-native controls and accessible states.
