# Swift Synchronization Primitive Review

## Problem/Feature Description

Review this synchronization plan for a Swift 6.3 app that supports iOS 16
through iOS 26:

- Use an actor for a synchronous metrics counter called from C callbacks.
- Put `NSLock` inside an actor for cache mutation.
- Hold a `Mutex` while awaiting a network fetch.
- Ban `NSLock` because it is not `Sendable`.

Replace it with a modern concurrency-safe plan.

## Output Specification

Create `synchronization-plan.md` with:

- When to choose actors, `Mutex`, `OSAllocatedUnfairLock`, and `Atomic`.
- The deployment-target tradeoff between `Mutex` and `OSAllocatedUnfairLock`.
- Corrections for locks inside actors and locks across `await`.
- A precise correction for the `NSLock` / `Sendable` claim.
