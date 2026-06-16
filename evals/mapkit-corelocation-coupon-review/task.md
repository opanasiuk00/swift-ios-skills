# Coupon Proximity Review

## Problem/Feature Description

A retail app team is building a MapKit-backed store locator that can highlight nearby coupon stores on the map and react when shoppers enter a store geofence. Their draft CoreLocation design creates monitoring objects from a SwiftUI map view, keeps dozens of coupon areas active, requests broad permission immediately, starts continuous location updates forever, and expects continuous background updates without a visible user-facing activity.

Review the MapKit/CoreLocation part of the design for an iOS 18+ implementation. Explain what should change, what architecture should own the monitoring lifecycle, and how the app should behave when location cannot be used normally. Keep notification delivery, ActivityKit UI, and background-processing mechanics out of scope except as handoff boundaries from the location feature.

## Output Specification

Create `location-review.md` with:

- A concise critique of the risky parts of the draft.
- A corrected architecture and permission/lifecycle plan.
- Any background-location requirements and degraded-state handling that should be part of the design.
