# APNs Registration Permission Review

## Problem/Feature Description

A SwiftUI app only calls `registerForRemoteNotifications()` after the user grants alert permission, stores the APNs device token in `UserDefaults` so future launches can skip server upload, and treats `didFailToRegisterForRemoteNotificationsWithError` on Simulator as a production bug.

## Output Specification

Create `apns-registration-review.md` with a concise correction-focused review. Cover the registration/authorization split, token handling, simulator testing, and the minimal SwiftUI/AppDelegate shape to use.
