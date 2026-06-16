# DockKit Custom Tracking Review

## Problem/Feature Description

Review this proposed DockKit custom tracking plan for mistakes:

- Keep system tracking enabled.
- Run Vision at 5 fps.
- Create `DockAccessory.Observation` rectangles in UIKit view coordinates.
- Call `track` once per second with an optional `CVPixelBuffer` when convenient.
- Animate the dock repeatedly in a tight loop until the subject is centered.

## Output Specification

Create a file named `dockkit-custom-tracking-review.md` containing:

- A correction-focused review of the plan.
- A corrected implementation shape for custom Vision/object tracking.
- Any important rate, coordinate, overload, and motor-control warnings.

Do not create an Xcode project. Keep the answer as implementation guidance and
snippets only.
