# DockKit Intelligent Tracking Boundary

## Problem/Feature Description

A camera app wants one feature that follows whichever person is speaking, shows
the dock battery in SwiftUI, reacts to dock zoom and shutter buttons, and pairs
a new BLE camera accessory if none is connected.

Explain what belongs in DockKit, what availability checks to use, and what
should move to another skill or framework.

## Output Specification

Create a file named `dockkit-boundary.md` containing:

- The DockKit-owned parts of the feature.
- The availability checks for tracking state, battery state, and accessory
  button events.
- The SwiftUI state-management boundary.
- The correct handoff for BLE accessory pairing/discovery.

Do not create an Xcode project. Keep the answer as implementation guidance and
snippets only.
