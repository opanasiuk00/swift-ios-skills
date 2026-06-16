# PDFKit Overlay Lifecycle Plan

## Problem/Feature Description

A document app wants an interactive drawing or note layer above each PDF page.
The team plans to set a `PDFPageOverlayViewProvider`, create overlay views as
pages appear, and save the final PDF after the user edits several pages.

Write the PDFKit-side architecture for provider ownership, overlay lifecycle,
per-page state, and saving the overlay results.

## Output Specification

Create `pdfkit-overlay-plan.md` with:

- A short ownership model for the overlay provider.
- The PDFPageOverlayViewProvider callbacks that matter.
- How state survives page scrolling and overlay view teardown.
- How overlay data becomes part of the saved PDF.
- Any sibling-skill handoff that applies if the overlay uses Apple Pencil tools.
