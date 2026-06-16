# Contacts Limited Access Review

## Problem/Feature Description

An iOS 26 SwiftUI contacts feature currently treats only `CNAuthorizationStatus.authorized` as usable. When authorization is `.limited`, the UI hides the contact list and tells the person to grant full access in Settings.

Review the approach and describe what should change for a Contacts-based app that can work with selected contacts.

## Output Specification

Create a file named `contacts-limited-access-review.md` containing:

- A corrected authorization-state handling section.
- A section describing what the app can and cannot access under limited authorization.
- A SwiftUI-oriented recommendation for letting the person add more contacts.
- A short boundary note comparing limited-access management with `CNContactPickerViewController`.
