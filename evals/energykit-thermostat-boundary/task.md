# Smart Thermostat EnergyKit Plan Review

## Problem/Feature Description

A smart-thermostat app wants to add a feature that reduces HVAC use during
unfavorable grid periods and summarizes the result later. A teammate wrote a
short plan claiming the feature should work for every home, does not need any
special target setup, and can fall back to app power telemetry if EnergyKit
does not return a summary.

The engineering manager needs a concise review that identifies the minimum
changes before implementation starts. Keep the answer centered on EnergyKit and
the thermostat use case.

## Output Specification

Create a file named `energykit-thermostat-review.md` containing:

- A correction-focused review of the plan.
- Swift-oriented guidance for querying guidance and reporting HVAC load.
- User-facing or privacy notes the product team needs to know.
- A brief list of framework boundaries for anything that does not belong to
  EnergyKit.
