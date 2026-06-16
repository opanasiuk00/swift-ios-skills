# RelevanceKit Meeting Widget

## Problem/Feature Description

A watchOS 26 app wants a Smart Stack experience that shows one card per
upcoming meeting only when that meeting is relevant. The app already has a
normal timeline widget that can stay pinned when no specific meeting is
relevant.

Build focused Swift-oriented guidance and snippets for the RelevanceKit-owned
part of this feature.

## Output Specification

Create a file named `relevancekit-meeting-widget.md` containing:

- The relevant-widget API shape for watchOS 26.
- A `RelevanceEntry` and `RelevanceEntriesProvider` sketch.
- Priority-ordered `WidgetRelevanceAttribute` creation with date clues.
- Preview and placeholder handling.
- Guidance for avoiding duplicate cards with the existing timeline widget.
