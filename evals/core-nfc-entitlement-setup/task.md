# Core NFC Setup Review

## Problem/Feature Description

The iOS team is preparing a Core NFC feature. The app needs to scan NDEF tags, read ISO 7816 identity cards by AID, and read a FeliCa transit tag. Their draft configuration includes:

- `com.apple.developer.nfc.readersession.formats = ["NDEF", "TAG"]`
- `NFCReaderUsageDescription`
- one ISO 7816 application identifier

Review the setup and explain what should change before implementation.

## Output Specification

Create a file named `core-nfc-setup-review.md` containing:

- The corrected entitlement and Info.plist checklist.
- Notes for ISO 7816 and FeliCa configuration.
- The reader-session availability checks the implementation should perform.
- Any stale or risky setup assumptions in the draft.

Keep the answer as implementation guidance. Do not create an Xcode project.
