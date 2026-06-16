# Energy Insight Query Fix

## Problem/Feature Description

An energy dashboard supports devices running the first iOS 26 release. A draft
screen tries to show the past week of charging impact with daily rows and a
cleaner-energy subtotal, but QA sees empty data on some devices and compile
concerns around one of the returned fields.

The app team needs a corrected implementation note and Swift-oriented snippet
for the query. Keep it focused on EnergyKit insight APIs and the availability
story; do not build a full dashboard.

## Output Specification

Create a file named `energykit-insights-fix.md` containing:

- The corrected query shape for a seven-day view.
- Availability notes for the fields used by the UI.
- Guidance for totals-only versus breakdown queries.
- A short table mapping insight granularity choices to valid time ranges.
