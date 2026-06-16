# Speech Recognition Boundary Routing

## Problem/Feature Description

A notes feature records a spoken note, transcribes it, detects the text language
and sentiment, translates a summary to Spanish, plays back the recording with
captions, and optionally uses Apple Intelligence to summarize it.

Explain which parts belong in the speech-recognition skill and which should be
handed to sibling skills.

## Output Specification

Create a file named `speech-recognition-boundary-routing.md` containing:

- The speech-recognition responsibilities.
- The correct handoffs for text analysis, translation, playback/caption UI, and
  Apple Intelligence summarization.
- A concise end-to-end pipeline showing where transcript text and timing data
  cross skill boundaries.

Do not create an Xcode project. Keep the answer as implementation guidance and
snippets only.
