# Swift Concurrency Diagnostic Remediation

## Problem/Feature Description

A SwiftUI app has Default Actor Isolation set to `MainActor`. After enabling
Swift 6.3, it sees diagnostics around:

- An `@Observable` `StickerModel` that conforms to an `Exportable` protocol.
- A `PhotoProcessor` async method used by the model.
- A legacy SDK imported with `@preconcurrency`.

Write a remediation plan that preserves current behavior, avoids
`@unchecked Sendable` unless truly justified, and states which parts belong in
`swift-concurrency` rather than architecture, navigation, or SwiftUI state
skills.

## Output Specification

Create `concurrency-diagnostics.md` with:

- The preferred fix for UI-bound protocol conformance diagnostics.
- How to decide whether `PhotoProcessor` stays on the caller's actor or moves
  to `@concurrent` background work.
- How to treat `@preconcurrency` imports.
- Sibling-skill handoffs for out-of-scope architecture, navigation, or SwiftUI
  state details.
