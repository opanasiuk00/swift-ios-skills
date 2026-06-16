# Core Bluetooth Background Plan Review

## Problem/Feature Description

Review this BLE background plan for an iOS app:

- Scan for all nearby peripherals using `nil` services while the app is in the
  background.
- Keep live RSSI updates by relying on `CBCentralManagerScanOptionAllowDuplicatesKey`.
- Advertise a local name from the phone while the app is backgrounded.
- Skip `bluetooth-peripheral` because the service was added before suspension.
- After relaunch, restore only the app-stored peripheral identifier.

Write a review note that identifies what is wrong and gives corrected Core
Bluetooth guidance.

## Output Specification

Create a file named `core-bluetooth-background-review.md` containing:

- A bullet-by-bullet review of the proposal.
- Correct background central scanning guidance.
- Correct background peripheral advertising and service-availability guidance.
- Correct state restoration guidance for central and peripheral managers.
- Any required Info.plist/background-mode configuration.
