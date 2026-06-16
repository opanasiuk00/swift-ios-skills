# PencilKit Sync Compatibility Plan

## Problem/Feature Description

A drawing app is adding cloud sync for editable PencilKit documents. Some customers will open drawings on current iPadOS releases, while others may open them on older devices for months after launch. Product wants modern ink behavior where possible, but support needs a clear plan for what happens when a drawing cannot safely round-trip to an older install.

Write the implementation guidance for the data model and canvas setup. The team needs enough Swift snippets to review the persistence, loading, compatibility, and fallback policy.

## Output Specification

Create `pencilkit-compatibility-plan.md` containing:

- A persistence and loading strategy for editable PencilKit drawings.
- A compatibility decision flow for syncing between newer and older OS versions.
- Swift snippets for the relevant canvas/tool-picker configuration.
- Notes on fallback previews or read-only behavior when editable content is not compatible.

Do not create an Xcode project. Keep the output to implementation guidance and snippets.
