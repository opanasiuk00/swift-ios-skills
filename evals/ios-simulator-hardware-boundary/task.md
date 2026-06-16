# Simulator Hardware Boundary

## Problem/Feature Description

A release-candidate checklist currently keeps these tests in iOS Simulator: camera capture, BLE pairing, barometer-based elevation, accelerometer controls, Face ID fallback, memory warning handling, iCloud sync, push notifications, and Metal performance.

Explain which checks can remain in Simulator, which must move to real hardware, and what the team should still verify on devices before release.

## Output Specification

Create `simulator-hardware-boundary.md` with a concise ownership split. Keep it focused on iOS Simulator limitations and avoid implementing Core Bluetooth, Core Motion, Push Notifications, Instruments, or Metal code.
