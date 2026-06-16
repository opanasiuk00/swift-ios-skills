# Spam Filter CallKit Boundary

## Problem/Feature Description

A spam-filter app needs caller ID and call blocking, wants to support iOS 26 call translation, and also has normal APNs auth-key rotation work. The team asks whether its Call Directory extension can look up each caller from its API as calls arrive and which parts belong in CallKit guidance versus sibling domains.

## Output Specification

Create `call-directory-boundary.md` with a boundary-aware answer. Keep implementation detail concise and route adjacent work to the right domain.
