# Account Security Scope Review

## Problem/Feature Description

A product team asked for a single iOS security checklist before starting a new
account and document-sharing project. The checklist needs to cover account
login, passkeys, app/device integrity, token storage, document encryption,
network transport, App Store submission, and hardware-backed keys.

The repo has several focused Apple-platform skills, and the maintainer wants a
scope review that prevents one security answer from expanding into every
neighboring domain.

## Output Specification

Create `scope-routing.md` with:

- what the security guidance should answer directly,
- what should be routed to neighboring Apple-platform skills,
- any availability notes that affect the encryption portion,
- and a short final routed checklist.

The scope review should cover these requested topics:

- Sign in with Apple
- passkey server verification
- App Attest assertions
- URLSession quantum-secure TLS
- custom end-to-end document encryption for iOS 26
- Keychain refresh-token storage
- Secure Enclave keys
- certificate pinning
- App Store privacy manifests
