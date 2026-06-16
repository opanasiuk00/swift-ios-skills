# Multi-Framework Location Experience

## Problem/Feature Description

A product team is combining several Apple-platform ideas into one feature pitch: a navigation-oriented map, an in-car surface, a lightweight flow launched from a place card, and BLE beacon/accessory pairing that starts when the user reaches a venue.

They need a scope memo before implementation begins. Identify which parts belong in the MapKit skill and which should be routed to adjacent Apple framework skills, while preserving the handoff points between the pieces.

## Output Specification

Create `scope-memo.md` with:

- The MapKit/CoreLocation responsibilities that should stay in this skill.
- The responsibilities that should be handled by sibling skills or framework-specific guidance.
- The handoff data or event boundaries between those areas.
