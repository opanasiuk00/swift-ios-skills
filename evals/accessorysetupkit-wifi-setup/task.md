# Wi-Fi Camera Setup Flow

## Problem/Feature Description

A camera accessory broadcasts a temporary setup network named with the prefix `CamLink-`. The iOS app needs to let users add a camera, then join the selected accessory network to continue setup in the app. The team wants the experience to feel like a trusted system setup flow and avoid asking for broad local network or wireless discovery access before the user picks a camera.

Design the Swift-side setup guidance for this flow. The same app also supports BLE cameras, but this task is specifically about the Wi-Fi setup-network path.

## Output Specification

Create a file named `wifi-camera-setup.md` containing:

- The target configuration needed before discovery.
- Swift snippets for the Wi-Fi discovery descriptor, picker display item, session event handling, and network join handoff.
- A short note explaining what AccessorySetupKit handles and what NetworkExtension handles.
- A short note explaining how the app should avoid presenting setup unexpectedly.

Do not include HomeKit, Matter, or general camera-streaming implementation.
