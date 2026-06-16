# RealityKit AR Camera Setup Review

## Problem/Feature Description

A SwiftUI app presents `RealityView` on every iPhone, has no `NSCameraUsageDescription`,
assumes a black camera view means the model failed to load, and says there is never
a device capability setting for RealityKit because RealityKit handles AR automatically.

## Output Specification

Create `realitykit-ar-camera-setup.md` with a concise correction-focused review.
Cover camera privacy, runtime AR support checks, user-facing fallback handling,
required-device capability tradeoffs, and `RealityViewCameraContent` AR/non-AR
behavior on iOS.
