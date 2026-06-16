# DockKit Camera Control Flow

## Problem/Feature Description

An iOS camera app needs to work well when the phone is mounted on a
DockKit-compatible motorized stand. The team wants a concise implementation
guide for setup, system tracking, tap-to-track, framing and region of interest,
manual pan/tilt controls, and dock hardware buttons.

## Output Specification

Create a file named `dockkit-camera-control.md` containing:

- The setup and privacy caveats the app target should account for.
- Swift-oriented guidance for observing dock/undock, enabling system tracking,
  selecting a tapped subject, setting framing/ROI, manual pan/tilt, and button
  events.
- Availability notes for hardware button events.
- A short review-notes section covering lifecycle, Simulator, and boundary
  risks.

Do not create an Xcode project. Keep the answer as implementation guidance and
snippets only.
