# MusicKit Library And Charts Review

## Problem/Feature Description

Review this MusicKit implementation plan for iOS 26:

- Fetch top songs with `MusicCatalogChartsRequest(kinds: [.mostPlayed], types: [Song.self])`.
- Add selected songs, albums, and playlist entries to the user's library whenever
  a button is tapped.
- Manually update `MPNowPlayingInfoCenter` for Apple Music songs played through
  `ApplicationMusicPlayer`.
- Expand the review into AVKit and CarPlay recommendations if anything touches
  audio playback.

Explain what should change and provide corrected snippets where useful.

## Output Specification

Create a file named `musickit-library-charts-review.md` containing:

- Correct chart request guidance.
- Required checks before library mutations.
- Scoped guidance for Now Playing metadata.
- A short note on which adjacent frameworks should remain out of scope.
