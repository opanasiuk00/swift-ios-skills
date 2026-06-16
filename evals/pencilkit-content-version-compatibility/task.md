# Ink Compatibility Review

## Problem/Feature Description

A drawing app syncs `PKDrawing` data through CloudKit. The team wants to let users pick watercolor, crayon, and reed inks, then set only `canvasView.maximumSupportedContentVersion = .version2` so iPadOS 16 clients can open every drawing.

Review the plan and write the corrected compatibility guidance.

## Output Specification

Create `pencilkit-compatibility-review.md` with:

- The content-version mapping that matters for current PencilKit.
- What happens when older systems load drawings containing unsupported inks.
- The correct use of `requiredContentVersion` and `maximumSupportedContentVersion`.
- Any availability boundaries for reed and custom tool picker items.
- A short migration checklist.
