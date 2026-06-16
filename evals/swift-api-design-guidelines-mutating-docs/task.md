# Text Buffer Public API Polish

## Problem/Feature Description

A small text-processing package is preparing its first stable release. Its `TextBuffer` type already works internally, but the public names and documentation were drafted before the team settled the API shape. The package author wants a final proposal for the public declarations before cutting a release.

The result should make the in-place operations and copy-returning operations obvious at the call site, and the documentation should be suitable for generated API docs.

## Output Specification

Create `text-buffer-api.md` containing:

- A revised Swift declaration for `TextBuffer`.
- Documentation comments for every public member shown.
- A short rationale for the operation pairs and any complexity documentation.
- No package scaffolding or implementation beyond the declaration body already implied by the sample.

## Input

```swift
public struct TextBuffer {
    public var totalCharacterCount: Int {
        lines.reduce(0) { $0 + $1.count }
    }

    public mutating func formSortLines()
    public func sortLines() -> TextBuffer

    public mutating func stripNewlines()
    public func strippedNewlines() -> TextBuffer

    public mutating func unionTags(_ tags: Set<String>)
    public func formUnionTags(_ tags: Set<String>) -> Set<String>
}
```
