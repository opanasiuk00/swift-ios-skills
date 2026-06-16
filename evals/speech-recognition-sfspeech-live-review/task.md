# SFSpeechRecognizer Live Dictation Review

## Problem/Feature Description

Review this proposed iOS live dictation plan:

- Request only `NSSpeechRecognitionUsageDescription`.
- Start `AVAudioEngine` immediately.
- Use `SFSpeechRecognizer` forever in one recognition task.
- Force `requiresOnDeviceRecognition` for every locale.
- Ignore availability changes.

Give corrected guidance and focused Swift snippets.

## Output Specification

Create a file named `speech-recognition-sfspeech-live-review.md` containing:

- The required privacy keys and permission flow.
- Correct startup ordering for speech authorization, microphone permission,
  audio session activation, audio engine, request, and task setup.
- Availability and on-device recognition checks.
- Duration-limit, restart, and cleanup guidance.
- A short list of issues in the original plan.

Do not create an Xcode project. Keep the answer as implementation guidance and
snippets only.
