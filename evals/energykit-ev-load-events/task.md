# EV Charging Energy Guidance Review

## Problem/Feature Description

A vehicle team is adding clean-energy charging to its iOS app. The current draft
fetches grid guidance for a saved home location, creates a charging schedule,
and reports one EV electricity event after charging finishes. A reviewer noticed
that the draft creates a fresh UUID while building the event metadata and does
not describe what to report while the vehicle is charging.

The team needs a correction-focused implementation note that keeps the scope on
EnergyKit. They already have their own charging backend and do not want a new
Xcode project.

## Output Specification

Create a file named `energykit-ev-review.md` containing:

- A short review of what is wrong with the current draft.
- Swift-oriented snippets or pseudocode for fetching guidance, building a
  schedule, and reporting EV electricity use.
- A compact production checklist for cadence, identity, privacy, and boundary
  concerns.

Keep the output as implementation guidance only.
