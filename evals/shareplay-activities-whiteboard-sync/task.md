# SharePlay Whiteboard Architecture Review

## Problem/Feature Description

A team proposes a collaborative whiteboard SharePlay design where every stroke is sent reliably, image drops are sent as Data through GroupSessionMessenger, late joiners rebuild from whatever messages they receive, and the sessions() listener lives in a SwiftUI view task.

## Output Specification

Create `shareplay-whiteboard-review.md` that identifies the architecture problems and proposes a corrected SharePlay design. Include message delivery choices, attachment handling, late-joiner state, retained session observation, and cleanup behavior.
