# Contacts Picker And Change Boundary Review

## Problem/Feature Description

An iOS 26 app needs a no-permission email picker and an incremental Contacts sync. The draft uses `CNContactPickerViewController` for email selection and calls `store.enumerateChanges(matching: CNChangeHistoryFetchRequest())` from Swift to process updates.

Review the API boundaries and give Swift-safe guidance.

## Output Specification

Create a file named `contacts-picker-change-boundary-review.md` containing:

- A section on contact-picker authorization and selection scope.
- A section on picker predicates for email-only selection.
- A section on why the change-history code is not safe as written.
- A Swift-safe fallback for keeping cached contacts current.
