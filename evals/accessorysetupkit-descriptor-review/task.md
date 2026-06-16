# Accessory Discovery Configuration Review

## Problem/Feature Description

A teammate drafted an accessory setup design for a thermostat hub app and wants a focused implementation review before it is handed to the iOS team. The plan includes one Wi-Fi hub variant and one BLE hub variant.

Draft plan:

```swift
var wifiDescriptor = ASDiscoveryDescriptor()
wifiDescriptor.ssid = "ThermoHub-123"
wifiDescriptor.ssidPrefix = "ThermoHub-"

var bleDescriptor = ASDiscoveryDescriptor()
bleDescriptor.bluetoothManufacturerDataMask = Data([0xFF, 0xF0])
bleDescriptor.bluetoothManufacturerDataBlob = Data([0xA0])
```

The app target currently declares only Bluetooth support in its property list. The team also wrote that "any nearby accessory with matching data can be shown by the picker."

## Output Specification

Create a file named `configuration-review.md` containing:

- A concise review of the crash risks and invalid assumptions in the draft.
- Corrected descriptor snippets for the Wi-Fi and BLE variants.
- The property list declarations the app target needs.
- A checklist reviewers can use before approving the implementation.

Keep it implementation-focused; do not write a general tutorial about Bluetooth or Wi-Fi.
