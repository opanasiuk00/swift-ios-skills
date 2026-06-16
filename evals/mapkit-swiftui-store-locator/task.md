# Neighborhood Store Locator

## Problem/Feature Description

A grocery chain is replacing a static list of locations with an iOS store locator. The first version should feel native in SwiftUI, let customers search near the visible map area, choose a result, inspect a compact detail surface, and see a route from their current location to the selected store.

The team wants a technical plan with enough Swift code to guide implementation. They also need the location privacy and lifecycle behavior called out because this screen will be embedded in an app that has other non-location shopping flows.

## Output Specification

Create `store-locator-plan.md` with:

- The recommended SwiftUI view/model structure.
- Representative Swift snippets for map rendering, search, marker selection, route drawing, and location handling.
- The Info.plist/privacy, denied-permission, and cancellation behavior the team should implement.
