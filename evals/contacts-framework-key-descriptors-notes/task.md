# Contacts Key Descriptor And Notes Review

## Problem/Feature Description

An iOS contacts feature plans to fetch displayed names with `CNContactCompleteNameKey`, load `CNContactImageDataKey` for every row in a list, and include `CNContactNoteKey` so notes can appear in a detail screen.

Review the plan before it ships.

## Output Specification

Create a file named `contacts-key-descriptor-notes-review.md` containing:

- Corrections for the displayed-name key descriptor choice.
- Guidance on image keys for list avatars.
- A notes-access entitlement section.
- A concise corrected `keysToFetch` example for a contact list.
