# Delivery Status on CarPlay

## Problem/Feature Description

A delivery app team wants order progress to appear in the car. The product brief mentions a Live Activity for the ETA, a small glanceable widget for CarPlay Home Screen, and a possible future in-car ordering flow.

Clarify which implementation domains should own these surfaces and whether the team should build the status experience with CarPlay templates.

## Output Specification

Create a file named `carplay-surface-boundary.md` containing:

- A clear ownership decision for Live Activity, widget, and template-based CarPlay app work.
- A short explanation of why the status surface should or should not be built with CarPlay framework templates.
- The CarPlay-specific validation concerns the team should still keep.
- A brief note about when a separate CarPlay template app flow might become appropriate.
