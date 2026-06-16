# Continued Photo Export

## Problem/Feature Description

A photo-editing app needs an iOS 26 export flow. The export starts only after a person taps an Export button, may take several minutes, should keep going if the app is backgrounded, and may use GPU-backed image processing when the device supports it.

## Output Specification

Create `continued-photo-export.md` with the recommended BackgroundTasks API, the identifier and Info.plist approach, progress/cancellation guidance, GPU resource checks, and any entitlement or capability requirements.
