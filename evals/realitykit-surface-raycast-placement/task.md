# Surface Raycast Placement Review

## Problem/Feature Description

A developer wants tap-to-place on a physical table. Their plan is to use
`SpatialTapGesture` with `RealityViewCameraContent.hitTest`, assume any hit is a
detected table surface, and create a world anchor at that point.

## Output Specification

Create `realitykit-surface-raycast-placement.md` with a source-grounded review
that distinguishes RealityKit entity hit testing from ARKit real-world surface
raycasts, then recommends the correct placement approach for detected planes and
one-shot physical-surface intersections.
