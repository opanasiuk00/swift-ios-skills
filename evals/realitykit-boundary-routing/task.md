# RealityKit Boundary Routing

## Problem/Feature Description

A team found a visionOS sample using `ARKitSession`, `WorldTrackingProvider`,
and `PlaneDetectionProvider`. They want to copy those APIs into an iOS
`RealityView` app and also migrate an older `SCNView`/`SCNNode` scene in the
same pass.

## Output Specification

Create `realitykit-boundary-routing.md` with a short architecture note. Explain
what belongs in the iOS RealityKit path, what is visionOS-specific, and how to
treat existing SceneKit node-based work without mixing incompatible scene graph
APIs.
