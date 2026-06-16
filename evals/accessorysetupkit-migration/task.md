# Legacy BLE Accessory Migration Plan

## Problem/Feature Description

An existing iOS app already has users who granted Bluetooth access before the app adopted the newer accessory setup flow. The app stores known `CBPeripheral` identifiers for paired badge readers. Product wants the next release to migrate these known readers into the new system-controlled accessory list without forcing users to rediscover every reader manually.

Write a migration plan and Swift implementation outline. The current prototype creates `CBCentralManager` during app startup and then tries to show the migration picker later.

## Output Specification

Create a file named `migration-plan.md` containing:

- A migration sequence for known BLE badge readers.
- Swift snippets showing how to create migration display items and handle session events.
- A section named `Startup changes` explaining what must change in the prototype.
- A section named `After migration` explaining when normal BLE communication can resume.

Do not build a full app or include unrelated UI code.
