# Hiking Motion Plan Review

## Problem/Feature Description

A hiking app team plans to use `CMPedometer` for daily steps,
`CMMotionActivityManager` to switch between walking and driving modes, and
`CMAltimeter` for elevation. Their draft says absolute altitude is GPS-based,
activity flags are mutually exclusive, and only activity recognition needs
motion permission.

## Output Specification

Create `core-motion-hiking-review.md` with a correction-focused review. Keep the
answer scoped to Core Motion unless a brief handoff to another Apple framework is
needed.
