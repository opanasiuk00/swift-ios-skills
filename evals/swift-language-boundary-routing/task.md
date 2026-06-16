# Swift Cleanup Routing Memo

## Problem/Feature Description

A maintainer is triaging cleanup requests before creating work items for a small iOS package. Some requests are about core language choices, while others overlap with adjacent Swift skills. They want one short routing memo that identifies who should own each concern and includes only enough code to make the language-level decision concrete.

## Output Specification

Create `swift-cleanup-routing.md` containing:

- A brief owner/domain for each cleanup item.
- Minimal examples are acceptable for handoffs, but avoid turning sibling-owned
  work into full implementations.
- Clear handoff guidance for sibling domains.

## Cleanup Items

1. Build complete API response models for a remote service, including snake_case key handling and timestamp decoding.
2. Design currency, date, and list display for several international markets.
3. Decide whether a reusable helper should expose protocol values with opaque types, existential values, or an impossible result/failure type.
4. Note any related handoff if the helper's public names and labels also need review.
