# SwiftUI Focus Plan Review

## Problem

A team is building an iPadOS document editor with a form and command menu. Their plan gives each `TextField` a separate Boolean `@FocusState`, reuses the same enum case for two different fields in a later refactor, sets several default focus targets on the same screen, and has toolbar commands read the selected document from global app state.

Review the plan and replace it with concise corrected guidance. Include Swift where it clarifies the recommended approach. Keep the answer focused on keyboard and scene focus behavior, not accessibility-specific focus.

## Output

Create a Markdown file named `focus-form-command-review.md`.
