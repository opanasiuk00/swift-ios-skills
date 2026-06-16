# Architecture Scope Boundary Routing

## Problem/Feature Description

A product lead asks for one architecture memo covering SwiftUI state ownership,
deep links and tab routing, actor isolation errors, app-wide module boundaries,
and test strategy.

Split what belongs in `ios-architecture` versus adjacent skills, then give the
architecture-level recommendation.

## Output Specification

Create `architecture-boundaries.md` with:

- The responsibilities that stay in `ios-architecture`.
- The responsibilities that should move to sibling skills.
- A concise architecture recommendation after the boundary split.
- Handoff points between architecture decisions and implementation details.
