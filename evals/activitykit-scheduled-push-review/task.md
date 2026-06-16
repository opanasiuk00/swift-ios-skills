# Flight Board Live Activity Plan Review

## Problem/Feature Description

A travel app team wrote a short plan for a flight-board Live Activity and wants a technical review before implementation. The plan says: schedule the board with `Activity.request(attributes:content:pushType:start:)`; make it `style: .transient` but guard that as an iOS 26-only API; omit the push-to-start alert because notification permission is already handled; enable frequent updates and send server pushes every 30 seconds; and tell product that ended activities disappear after 8 hours.

## Output Specification

Create `flight-live-activity-review.md` with a correction-focused review. Include corrected Swift or payload snippets only where they clarify the review.
