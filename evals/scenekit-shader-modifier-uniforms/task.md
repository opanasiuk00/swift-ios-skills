# SceneKit Shader Modifier Fix

## Problem/Feature Description

A legacy SceneKit screen animates a material with this shader modifier code:

```swift
material.shaderModifiers = [
    .geometry: "_geometry.position.y += sin(scn_frame.time);"
]
material.setValue(Float(scn_frame.time), forKey: "elapsed")
```

The team wants the modifier to animate over time and also wants Swift to pass a
custom amplitude value.

Fix the snippet and explain the correct boundary between SceneKit shader
modifiers and lower-level custom Metal shader functions.

## Output Specification

Create a file named `scenekit-shader-modifier-fix.md` containing:

- corrected Swift and shader modifier snippets;
- a concise explanation of built-in time handling;
- a concise explanation of custom values passed from Swift;
- a note about where `scn_frame` belongs.

Do not create a full sample app.
