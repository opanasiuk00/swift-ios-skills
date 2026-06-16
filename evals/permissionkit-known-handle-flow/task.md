# PermissionKit Known-Handle Flow Correction

## Problem/Feature Description

An iOS team wrote a PermissionKit communication flow that calls
`isKnownHandle(_:)` before showing an Ask button and treats `false` as proof
that communication limits are enabled. The code then calls
`AskCenter.shared.ask` without handling `communicationLimitsNotEnabled`, and
the UI waits forever for a `PermissionResponse` after every tap.

The team needs corrected Swift-level guidance and pseudocode.

## Output Specification

Create a file named `permissionkit-known-handle-flow.md` containing:

- The correct meaning of `isKnownHandle(_:)` and `knownHandles(in:)`.
- The required fallback/error handling around `AskCenter.shared.ask`.
- The response-observation pattern for parent decisions.
- UI state guidance for pending requests where no response arrives.
