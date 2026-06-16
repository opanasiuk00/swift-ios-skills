# Simulator Launch, Push, and Privacy Review

## Problem/Feature Description

Review this proposed Simulator CI plan:

- Start the app with `xcrun simctl spawn booted env FEATURE_FLAG=1 /path/MyApp.app/MyApp`.
- Use `simctl push` as proof that APNs and all notification types work.
- Grant every privacy permission in CI and remove the app's usage description strings because CI no longer shows prompts.

## Output Specification

Create `simulator-launch-push-privacy-review.md` with corrected guidance. Cover app launch environment variables, what simulated push does and does not prove, push payload constraints when relevant, and the privacy/Info.plist caveat.

Keep the answer focused on iOS Simulator command-line testing.
