# Swift Concurrency Build Settings Review

## Problem/Feature Description

An iOS 26 app team is enabling Swift 6.3 in Xcode 26. Their draft plan says:

- Turn on Approachable Concurrency and the whole module becomes MainActor.
- Start Swift 6 strict concurrency at Targeted so warnings do not block the build.
- Leave CPU-heavy image decoding on MainActor because nonisolated async functions
  now hop to a background executor.

Review and correct the plan. Give the smallest build-setting and code-level
recommendations that preserve behavior while avoiding UI hangs.

## Output Specification

Create `concurrency-build-settings.md` with:

- Correct Xcode build-setting names and relationships.
- How strict concurrency behaves in Swift 6 / 6.3 language mode.
- When to use `@concurrent` and `nonisolated` for CPU-heavy work.
- Any migration caveats that apply only before Swift 6 language mode.
