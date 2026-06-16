# Background NFC Tag Routing Checklist

## Problem/Feature Description

A product manager wants an NFC tag to wake the app in the background by putting the app bundle ID and a custom content type in an NDEF record. They also asked whether a custom `myapp://` URL is fine for app-specific routing.

Write the corrected iOS implementation checklist.

## Output Specification

Create a file named `background-tag-routing.md` containing:

- The NDEF record shape background tag reading requires.
- The recommended app-specific routing setup.
- Unsupported routing assumptions to reject.
- The `NSUserActivity` handling path for delivered tag data.

Do not create an Xcode project.
