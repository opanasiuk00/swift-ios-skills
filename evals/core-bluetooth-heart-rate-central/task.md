# Core Bluetooth Heart Rate Central

## Problem/Feature Description

An iOS team is building a heart-rate monitor screen. The app should scan for
BLE peripherals advertising Heart Rate service `180D`, connect to the selected
peripheral, subscribe to Heart Rate Measurement characteristic `2A37`, parse the
BPM value, and send a small command to a writable characteristic when the user
taps a control.

Write implementation guidance for iOS 26 that shows the Core Bluetooth manager
shape and the safety checks needed for production BLE communication.

## Output Specification

Create a file named `core-bluetooth-heart-rate-guide.md` containing:

- Required Info.plist / authorization and manager-state checks.
- A Swift central-manager outline for scanning, retaining, connecting, service
  discovery, characteristic discovery, and notification subscription.
- A heart-rate measurement parser.
- A safe write helper that chooses the write type and handles write flow
  constraints.
- A short list of review notes for common failure modes.
