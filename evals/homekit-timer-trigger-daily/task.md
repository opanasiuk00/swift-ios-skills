# HomeKit Nightly Automation

## Problem/Feature Description

An iOS app manages a user's HomeKit home and needs a nightly "Good Night"
automation at 10:30 PM. The app should create the scene/action set, write a
few accessory characteristics, attach a daily timer trigger, and enable it.

## Output Specification

Create a file named `homekit-nightly-automation.md` containing:

- The HomeKit setup and authorization prerequisites.
- Swift-oriented guidance for creating the action set and characteristic write
  action.
- Swift-oriented guidance for creating a repeating 10:30 PM timer trigger,
  attaching the action set, and enabling the trigger.
- A short timing gotchas section.

Do not include Matter commissioning or AccessorySetupKit setup guidance.
