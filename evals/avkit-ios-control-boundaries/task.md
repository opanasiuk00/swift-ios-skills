# iOS AVKit API Boundary Review

## Problem/Feature Description

An iOS 26 implementation uses `playerVC.isSkipForwardEnabled`, `playerVC.isSkipBackwardEnabled`, `playerVC.skippingBehavior = .skipItem`, `playerVC.allowedSubtitleOptionLanguages`, `playerVC.requiresFullSubtitles`, and direct `playerItem.interstitialTimeRanges = [...]` assignment to support skip buttons, subtitle restrictions, and ad breaks.

Review the implementation and explain what should change for iOS.

## Output Specification

Create a file named `ios-avkit-boundary-review.md` containing:

- A section for transport control changes.
- A section for subtitle/closed-caption handling changes.
- A section for interstitial/ad-break handling changes.
- Swift snippets for the iOS-safe replacement patterns.
- A concise list of the original API boundary mistakes.
