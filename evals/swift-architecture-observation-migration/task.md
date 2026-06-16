# Legacy UIKit and Observation Migration

## Problem/Feature Description

An iOS 16-era UIKit-heavy app uses Coordinators, `ObservableObject` view models,
and a few VIPER modules. New features are SwiftUI on current OS targets, but
the old modules are still shipping.

Write a migration plan that modernizes Observation and architecture choices
without forcing one pattern across the entire app.

## Output Specification

Create `architecture-migration.md` with:

- How to migrate UI-observed state from `ObservableObject` to `@Observable`
  where the deployment target allows it.
- What should happen to existing Coordinator and VIPER modules.
- How new SwiftUI modules should choose among MV, MVVM, TCA, and Clean
  Architecture.
- Boundary handoffs for detailed concurrency, navigation, and testing work.
