# iOS Simulator Custom Route Script

## Problem/Feature Description

An iOS maps app team wants a repeatable command-line Simulator script for a route-following UI test. The script should choose or create a suitable simulator, boot it, install a simulator build of the app, run a two-point route without a GPX file, and leave the simulator in a clean state.

## Output Specification

Create `ios-simulator-route-script.md` with:

- The `simctl` commands or shell outline for selecting/creating, booting, installing, launching, driving the route, and cleanup.
- Notes on `.app` versus `.ipa`, UDID selection, and permission setup.
- The correct command-line route mechanism for custom waypoints.
- Cleanup steps that prevent later tests from inheriting state.

Keep the answer focused on Simulator and `simctl`; do not create an Xcode project.
