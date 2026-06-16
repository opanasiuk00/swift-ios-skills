# Silent Push Refresh Review

## Problem/Feature Description

A chat backend team wants to send silent pushes every few minutes so the app always has fresh messages. Another engineer proposes `apns-priority: 10` to make those pushes arrive immediately. The app should not redesign its visible notification UI as part of this review.

## Output Specification

Create `silent-push-refresh-review.md` with a correction-focused review of the server cadence, APNs payload/headers, app capability, and app delegate completion behavior.
