# BrowserEngineKit API Correction Review

## Problem/Feature Description

A code review found several BrowserEngineKit snippets written from stale assumptions:

- `WebContentExtension` is declared as `final class MyWebContentExtension: WebContentExtension { override func handle(...) }`.
- The XPC event handler calls `xpc_connection_resume`.
- File access sends a `.withSecurityScope` bookmark and calls `startAccessingSecurityScopedResource()` in the extension.
- Memory transfer entitlements are set to `true`.
- The rendering extension enables `.coreML` without an availability check.

Correct the snippets for iOS 26 and explain the important API details.

## Output Specification

Create `browserenginekit-api-corrections.md` with corrected Swift or entitlement snippets for each issue.
