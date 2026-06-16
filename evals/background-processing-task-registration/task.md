# Background Task Setup Review

## Problem/Feature Description

An iOS team has a SwiftUI app that registers a `BGAppRefreshTask` from a view's `.task` modifier. The app also submits a `BGProcessingTaskRequest` for database cleanup, but the submitted identifier is not listed in the app's property list. The handler starts async work and returns without an expiration handler.

## Output Specification

Create `background-task-setup-review.md` with a concise correction-focused review. Include corrected Swift and Info.plist snippets where they make the review clearer.
