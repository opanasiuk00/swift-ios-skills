# CryptoTokenKit Smart Card Extension Review

## Problem/Feature Description

A team wrote this plan for certificate-based smart-card login and wants a correction-focused review before implementation:

- Create an iOS token driver target with `TKTokenDriver`.
- Put `com.apple.ctk.driver-class` at the top level of `Info.plist`.
- Share one PIN-authenticated state across all token sessions.
- Register the extension by launching the normal app as the current user.

## Output Specification

Create `cryptotokenkit-token-extension-review.md` with the issues, corrected behavior, and any minimal snippets needed to make the guidance actionable.
