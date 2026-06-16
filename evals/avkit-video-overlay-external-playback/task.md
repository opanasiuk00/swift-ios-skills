# VideoPlayer Overlay and External Playback Review

## Problem/Feature Description

A SwiftUI iOS screen uses:

```swift
VideoPlayer(player: player) {
    Button("Buy") { purchase() }
}
```

The same setup also sets `player.usesExternalPlaybackWhileExternalScreenIsActive = true` because the developer believes it is required for AirPlay.

Review the snippet and explain the correct AVKit behavior.

## Output Specification

Create a file named `video-overlay-external-playback-review.md` containing:

- Whether the `VideoPlayer` overlay can be interactive.
- How that overlay relates to system playback controls and event handling.
- When to use `allowsExternalPlayback`.
- When to use `usesExternalPlaybackWhileExternalScreenIsActive`.
- A corrected snippet or checklist.
