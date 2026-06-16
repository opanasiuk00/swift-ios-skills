# CallKit Plan Review

## Problem/Feature Description

A VoIP team wrote this plan and wants a correction-focused review before implementation:

- When the user taps Answer, call `action.fulfill()` immediately, then connect WebRTC.
- Start the audio engine before `provider(_:didActivate:)`.
- Send another VoIP push if the caller hangs up.
- For encrypted payloads, always use `CXProvider.reportNewIncomingVoIPPushPayload` from a notification service extension.

## Output Specification

Create `callkit-plan-review.md` with the issues, corrected behavior, and any minimal snippets needed to make the guidance actionable.
