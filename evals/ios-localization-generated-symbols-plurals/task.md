# String Catalog Generated Symbols and Plurals

## Problem/Feature Description

A SwiftUI booking app is moving to `Localizable.xcstrings`. It has a manually managed key named `room_available` whose English value is "Book this room" and a parameterized key named `landmarks_count` for text like "42 landmarks".

The team wants to use Xcode generated localizable symbols, keep plural handling ready for translators, and modernize old `NSLocalizedString` call sites without making incorrect deployment-target claims.

## Output Specification

Create `localization-generated-symbols.md` with a concise migration plan and Swift snippets. Include generated-symbol usage, the catalog placeholder syntax, modern string API guidance, and what to do with legacy `NSLocalizedString` calls.
