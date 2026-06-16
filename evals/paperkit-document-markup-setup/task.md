# Document Markup Screen

## Problem/Feature Description

The document team is adding an iPadOS 26 review screen where a user can draw over a rendered page, add callouts and labels, keep the system drawing palette visible, and return later with the annotations restored. The screen is hosted from SwiftUI, but the markup surface can use UIKit where appropriate.

The design review also asked whether bright HDR colors should be supported on devices that can display them. The team wants implementation guidance that is practical enough for a first code review, not a full app.

## Output Specification

Create a file named `paperkit-document-markup-plan.md` containing:

- A concise architecture note.
- Swift snippets for the SwiftUI bridge, markup controller setup, insertion UI, tool picker setup, persistence, and HDR color support.
- A short review checklist for the team before shipping.
