# AudioAccessoryKit Snippet Review

## Problem/Feature Description

An engineer found this sample in an internal setup guide and wants to know
whether it still matches the current AudioAccessoryKit API and lifecycle.

```swift
let capabilities: AccessoryControlDevice.Capabilities = [.audioSwitching, .placement]
try await AccessoryControlDevice.register(accessory, capabilities)
let device = try AccessoryControlDevice.current(for: accessory)
var config = device.configuration
config.devicePlacement = .inEar
try await device.update(config)
```

Review the snippet and provide a corrected version if needed. Keep the answer
focused on AudioAccessoryKit and the framework ownership boundaries.

## Output Specification

Create a file named `audioaccessorykit-snippet-review.md` containing:

- whether the snippet is current or stale;
- a corrected registration example;
- a corrected placement update example;
- a short explanation of where each operation belongs; and
- any important caveats about the `ASAccessory` value.
