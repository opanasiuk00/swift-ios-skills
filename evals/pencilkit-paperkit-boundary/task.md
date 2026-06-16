# Annotation Framework Boundary

## Problem/Feature Description

An annotation feature needs freehand Apple Pencil signatures, movable text boxes, arrows, image stickers, and a system-standard markup toolbar. The team is unsure whether to implement everything with PencilKit or split responsibilities with PaperKit.

Write a short architecture note that assigns responsibilities to the right framework and explains the handoff points.

## Output Specification

Create `pencilkit-paperkit-boundary.md` with:

- What belongs in PencilKit.
- What belongs in PaperKit.
- The bridge points between `PKDrawing`, `PKTool`, and PaperKit markup.
- A short list of mistakes to avoid.
