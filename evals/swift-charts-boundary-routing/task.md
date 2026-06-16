# Swift Charts Boundary Routing

## Problem/Feature Description

A dashboard request mixes several concerns:

- Swift Charts mark selection, axes, legends, scrolling, vectorized plots, and
  a possible iOS 26 3D view.
- MapKit annotations.
- `NavigationStack` deep links.
- Async data loading and `@Observable` model ownership.
- A custom VoiceOver audit.

Split what belongs in the `swift-charts` skill versus adjacent Apple skills,
then give the chart-specific recommendations.

## Output Specification

Create `charts-boundary-routing.md` with:

- The chart-specific work that belongs in `swift-charts`.
- Which adjacent skills should own map, navigation, data loading, state
  architecture, and deep accessibility details.
- A concise set of Swift Charts implementation recommendations for the
  dashboard.
