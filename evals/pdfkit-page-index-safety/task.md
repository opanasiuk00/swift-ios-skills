# PDFKit Page Index Review

## Problem/Feature Description

An iOS team has a PDF viewer with buttons that jump to a selected page, remove
the selected page, insert a new blank page, and swap two pages. Their current
implementation calls `document.page(at:)`, `removePage(at:)`,
`insert(_:at:)`, and `exchangePage(at:withPageAt:)` directly from UI state.

Review the approach and provide corrected Swift snippets for the unsafe parts.

## Output Specification

Create `pdfkit-page-index-review.md` with:

- The page-index rule an implementation must follow.
- Corrected page navigation code.
- Corrected remove, insert, and exchange helpers.
- A short explanation of what not to rely on when using `page(at:)`.
