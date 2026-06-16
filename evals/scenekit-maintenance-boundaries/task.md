# SceneKit Maintenance Snippet Audit

## Problem/Feature Description

During maintenance of an existing SceneKit app, a review finds these snippets
and a broader feature proposal:

```swift
scene.setAttribute(["UnitMetersPerUnit": 1.0],
                   forKey: SCNScene.Attribute.unit.rawValue)

node.physicsBody = SCNPhysicsBody(
    type: .dynamic,
    shape: SCNPhysicsShape(geometry: mesh)
)
```

The same change list also proposes rewriting gameplay scoring with GameKit
while touching the 3D scene graph.

Audit the snippets and proposal. Explain what should change and where related
work should be handed off.

## Output Specification

Create a file named `scenekit-maintenance-audit.md` containing:

- corrections for the scene attribute/unit handling;
- a corrected physics-shape snippet;
- a short note on GameKit scope and handoff;
- any SceneKit maintenance caveats needed for the review.

Do not create a full game architecture document.
