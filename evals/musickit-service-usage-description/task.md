# MusicKit Setup Review

## Problem/Feature Description

An iOS 26 app team is preparing to add Apple Music search and playback. Their
setup checklist currently says:

- Add a `com.apple.developer.musickit` entitlement in Xcode.
- Skip `NSAppleMusicUsageDescription` because the app only searches Apple Music.
- Call `MusicAuthorization.request()` during app launch.
- Expect authorization to crash when the MusicKit entitlement is missing.
- Add background audio immediately, even before deciding whether playback should
  continue in the background.

Review the checklist and provide corrected implementation guidance.

## Output Specification

Create a file named `musickit-setup-review.md` containing:

- The corrected Apple Developer portal / bundle ID setup.
- The required Info.plist usage description guidance.
- Correct authorization timing and status-check guidance.
- A short list of false assumptions in the original checklist.
