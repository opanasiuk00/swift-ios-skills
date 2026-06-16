# BLE Sensor Onboarding Design

## Problem/Feature Description

The mobile team is adding first-run setup for a new iOS environmental sensor. The sensor advertises a Bluetooth LE GATT service `12345678-1234-1234-1234-123456789ABC` and its advertised name begins with `EnviroTag`. Product wants setup to feel like a system-mediated pairing flow instead of asking users for broad wireless permissions.

Design the app-side Swift implementation for onboarding this sensor. The app should remember previously approved sensors, present setup from an Add Sensor button, and continue with a short in-app calibration step after the system UI closes.

## Output Specification

Create a file named `ble-sensor-setup.md` containing:

- The Info.plist keys and values the app target should declare.
- Swift snippets for the session manager, discovery descriptor, picker display item, picker presentation, event handling, and post-selection Bluetooth connection handoff.
- A short "review notes" section explaining permission behavior and any lifecycle/order constraints the implementation relies on.

Do not create an Xcode project. Keep the answer as implementation guidance and snippets only.
