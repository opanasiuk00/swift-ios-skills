# Background Push Payload Review

## Problem/Feature Description

A backend team wants to send silent pushes every few minutes so chat data is always fresh. Another engineer proposes `apns-priority: 10` to make the pushes arrive immediately. The visible notification UI is already designed elsewhere.

## Output Specification

Create `background-push-review.md` with a correction-focused review of the APNs payload, APNs headers, app capability, app delegate completion behavior, and boundary handoffs. Do not redesign visible notification UI.
