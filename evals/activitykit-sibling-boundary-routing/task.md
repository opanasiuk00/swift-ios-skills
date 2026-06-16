# Live Activity Ownership Boundaries

## Problem/Feature Description

A team owns a Live Activity that receives server updates, but their current request mixes several adjacent topics: rotating the APNs authentication key, registering ordinary remote notifications, deciding whether a widget should use a timeline provider, and adjusting the Live Activity payload itself. They need a short routing note so engineers know which guidance to follow for each part without conflating the domains.

## Output Specification

Create `live-activity-boundaries.md` with a concise ownership map and recommendations. Keep it as guidance only; do not produce implementation code.
