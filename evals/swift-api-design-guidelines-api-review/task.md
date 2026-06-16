# Design System API Review

## Problem/Feature Description

A team is extracting a small design-system palette from an app into a reusable Swift module. The current public API was named quickly during prototyping and now appears in sample code and partner docs. Before the package is published, they want the surface reviewed for names, argument labels, and call-site readability.

The API should feel idiomatic to Swift developers and should be easy to understand when reading a call site without jumping to the declaration.

## Output Specification

Create `api-design-review.md` containing:

- A revised Swift API declaration for `ThemePalette`.
- Revised example call sites for the two sample calls.
- A concise rationale for each renamed declaration or label.
- No Xcode project or package scaffolding.

## Input

```swift
public struct ThemePalette {
    public mutating func add(color: UIColor)
    public mutating func remove(index: Int) -> UIColor
    public func colorWithName(_ string: String) -> UIColor?
    public func containsColor(_ color: UIColor) -> Bool
    public static func createDefaultPalette() -> ThemePalette
}

let palette = ThemePalette.createDefaultPalette()
palette.colorWithName("warning")
```
