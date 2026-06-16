# BLE Thermostat Setup Boundary

## Problem/Feature Description

A team is designing first-run setup for a BLE thermostat. They want a
privacy-preserving picker for discovery and user approval. After the user picks
the thermostat, the app needs to read and write GATT services and
characteristics.

Write a routing note explaining whether this should be implemented entirely with
Core Bluetooth, entirely with AccessorySetupKit, or split across both domains.

## Output Specification

Create a file named `core-bluetooth-ask-boundary.md` containing:

- The recommended split of responsibility.
- What AccessorySetupKit owns during first-run setup.
- What Core Bluetooth owns after selection.
- What not to route to each domain.
- A short handoff sequence from selected accessory to BLE communication.
