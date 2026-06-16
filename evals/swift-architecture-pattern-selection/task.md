# SwiftUI Architecture Selection

## Problem/Feature Description

A small iOS 26 SwiftUI team is starting a trip-planning app with three CRUD
screens, search, a little async loading, and no shared navigation requirements
yet. They are debating MVVM, Clean Architecture, TCA, and VIPER because those
sound more testable than a simple model-view setup.

Review the architecture choice and recommend the smallest pattern that still
keeps the code testable. Include when the team should escalate to a heavier
pattern.

## Output Specification

Create `architecture-selection.md` with:

- The recommended starting architecture and why it fits.
- Why the heavier patterns should not be the default for this feature.
- Concrete escalation triggers for MVVM, TCA, Clean Architecture, and
  Coordinator.
- Any sibling-skill handoffs for detailed SwiftUI state or navigation
  implementation.
