# RelevanceKit Boundary Routing

## Problem/Feature Description

A team wants one answer covering an iOS Home Screen widget timeline, watchOS
Smart Stack relevance, HealthKit workout recording, MapKit place search, and
APNs widget push updates.

They need a scope memo before implementation starts. Identify what belongs in
the RelevanceKit skill and what should be routed to sibling Apple framework
skills.

## Output Specification

Create a file named `relevancekit-boundaries.md` containing:

- The RelevanceKit-owned responsibilities.
- The work that should move to WidgetKit.
- The work that should move to HealthKit.
- The work that should move to MapKit/CoreLocation.
- The handoff points between those domains.
