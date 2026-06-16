# Swift Cleanup Routing

## Problem/Feature Description

A package maintainer is triaging several cleanup requests before opening issues for the team. One item is a public function name that reads awkwardly in sample code. Another is a return-type design question involving protocol values. A third is about enforcing naming rules consistently in CI.

The maintainer wants one short routing memo that says which domain should own each concern and gives only the minimum concrete example needed to clarify the API naming item.

## Output Specification

Create `swift-cleanup-routing.md` containing:

- A brief owner/domain for each cleanup item.
- A minimal corrected example for the API naming item.
- Clear handoff guidance for the other two items.
- No full lint configuration, no full protocol type-system tutorial, and no package scaffolding.

## Cleanup Items

```swift
public protocol UserRepository {
    func fetchDataWithId(_ id: String) async throws -> UserData
    func makeSearchSource() -> any SearchSource
}
```

The CI request is: "Make the linter enforce our identifier naming choices."
