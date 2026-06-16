# Swift Package Localization Bundle Lookup

## Problem/Feature Description

The `SharedUI` Swift package has `Resources/Localizable.xcstrings`, and `Package.swift` includes `.process("Resources")`. Inside the package target, code currently uses `Text("Save")` and `String(localized: "settings.title")` with no bundle argument.

In the app target the same keys localize, but inside the package they fall back to English.

## Output Specification

Create `package-localization-review.md` that explains the likely problem and the minimal changes to make package-owned strings resolve from the package resource bundle. Keep the response scoped to localization bundle lookup.
