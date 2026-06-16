# PDFKit Feature Boundary Memo

## Problem/Feature Description

A team is designing a document feature that displays PDFs, fills form fields,
shows page thumbnails, wraps the viewer in SwiftUI, supports Apple Pencil
markup, and may later move to the system markup UI.

They need a scope memo before implementation starts. Identify what belongs in
the PDFKit skill and what should be routed to sibling Apple framework skills.

## Output Specification

Create `pdfkit-boundary-memo.md` with:

- The responsibilities that stay in PDFKit.
- The responsibilities that should move to SwiftUI/UIKit interop guidance.
- The responsibilities that should move to PencilKit or PaperKit guidance.
- The handoff points between those domains.
