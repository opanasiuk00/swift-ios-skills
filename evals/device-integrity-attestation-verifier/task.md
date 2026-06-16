# App Attest Attestation Verifier

## Problem/Feature Description

An iOS backend team is adding App Attest enrollment. The app sends a `keyId`, an `attestationObject`, and the challenge it received from the server. The server needs a verifier design before it stores any key material or marks the device as enrolled.

## Output Specification

Write a concise verification checklist for the server implementation. Focus on the data that must be decoded, the cryptographic and app-identity checks, replay defenses, and what should be persisted only after successful verification.
