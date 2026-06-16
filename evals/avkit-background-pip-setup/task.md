# AVKit Playback Setup Review

## Problem/Feature Description

An iOS team is reviewing a proposed video player setup. The code calls `AVAudioSession.setCategory(.playback, mode: .moviePlayback)` and `setActive(true)` during app launch, does not declare any background modes, and assumes `AVPlayerViewController` will make Picture in Picture and AirPlay work automatically.

Review the setup and provide corrected implementation guidance for iOS 26.

## Output Specification

Create a file named `avkit-playback-setup-review.md` containing:

- The required target capability / Info.plist configuration.
- Correct Swift snippets for audio session configuration and activation timing.
- Notes about standard `AVPlayerViewController` PiP and AirPlay behavior.
- A short list of issues in the original proposal.
