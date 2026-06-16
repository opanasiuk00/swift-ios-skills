# SwiftUI PencilKit Tool Picker Repair

## Problem/Feature Description

An iPad note-taking app has a SwiftUI screen that embeds a PencilKit canvas through `UIViewRepresentable`. The floating drawing palette appears, but selecting a different tool in the palette does not change what the canvas draws. The team also wants the answer to explain how the input policy should be described for Pencil-first, finger-drawing, and system-default behavior.

They need implementation guidance they can paste into an engineering design note before rewriting the wrapper.

## Output Specification

Create `swiftui-pencilkit-wrapper.md` containing:

- A corrected SwiftUI wrapper or focused code sketch.
- The lifecycle details that make the palette and canvas stay connected.
- A short review checklist for the drawing policy and state synchronization.

Do not create an Xcode project. Keep the output to Swift snippets and implementation guidance.
