# Device Integrity Plan Review

## Problem/Feature Description

A team proposes this device-integrity plan: cache a `DCDevice` token for the full install, use one App Attest key for every account on a device, retry failed attestation by immediately creating a new key, treat `invalidKey` as an OS update issue, and include OAuth tokens plus certificate pinning in the same checklist.

## Output Specification

Write a concise correction list. Keep the guidance focused on DeviceCheck and App Attest, and call out which adjacent security topics should be handed to sibling authentication, networking, or security work.
