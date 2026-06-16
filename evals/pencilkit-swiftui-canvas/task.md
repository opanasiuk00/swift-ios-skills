# Drawing Screen Implementation

## Problem/Feature Description

An iPad note-taking app needs a SwiftUI screen where users can draw with Apple Pencil, optionally enable finger drawing, show the PencilKit tool picker, and persist the drawing between launches.

Prepare an implementation note for the team. Focus on the PencilKit and SwiftUI interop details that prevent stale tools, missing picker updates, or state synchronization loops.

## Output Specification

Create `pencilkit-canvas-note.md` with:

- A `UIViewRepresentable` sketch for `PKCanvasView`.
- Tool picker setup and lifecycle notes.
- Drawing policy guidance for Pencil-primary and finger-drawing modes.
- Save/load snippets for `PKDrawing`.
- A short review checklist of mistakes to avoid.
