# PermissionKit Availability and iMessage Setup Review

## Problem/Feature Description

A family communication app supports iOS 26.0 and iPadOS 26.0. A draft
PermissionKit setup uses `PermissionButton` and `AskCenter` everywhere without
availability checks, says parent approval can be routed through the app's own
DM system, and adds a custom `com.apple.developer.permissionkit` entitlement.

The team needs corrected implementation guidance before starting the feature.

## Output Specification

Create a file named `permissionkit-setup-review.md` containing:

- PermissionKit API availability by 26.0, 26.1, and 26.2 groups.
- The communication-channel limitation that affects the product design.
- Setup guidance for imports, capabilities, and entitlement assumptions.
- A short boundary note explaining what PermissionKit does not own.
