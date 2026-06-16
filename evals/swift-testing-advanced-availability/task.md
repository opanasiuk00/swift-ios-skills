# Swift Testing Advanced API Review

## Problem/Feature Description

A developer targeting iOS 26 with Swift 6.3 wrote Swift Testing samples using `#expect(exitsWith: .failure)` in an exit-test closure that reads a local `expectedCode`, `Test.cancel()` in a synchronous test that awaits a network check, `Issue.record(severity: .warning)`, and `Attachment(image, named:).record()`. They need current API spelling, availability, platform support, which pieces are Swift 6.2 / Xcode 26.0 versus Swift 6.3 / Xcode 26.4-era APIs, and code-shape fixes.

## Output Specification

Create `swift-testing-advanced-api-review.md` with a concise review, corrected Swift snippets where useful, and any platform/toolchain caveats. Do not create an Xcode project.
