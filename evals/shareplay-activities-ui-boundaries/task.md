# SharePlay Launch Surface and Boundary Plan

## Problem/Feature Description

An app team wants a SharePlay launch path that works from a normal SwiftUI share button, over AirDrop when people are nearby, and from a custom UIKit button when no FaceTime call is active. They also want to know which parts belong in GameKit, TabletopKit, or AVKit instead of the SharePlay layer.

## Output Specification

Create `shareplay-ui-boundaries.md` with a launch-surface plan, Transferable guidance, GroupActivitySharingController usage, discoverability notes, and clear boundaries for GameKit, TabletopKit, and AVKit handoffs.
