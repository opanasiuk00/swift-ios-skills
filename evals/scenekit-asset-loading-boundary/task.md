# SceneKit Asset Loading Review

## Problem/Feature Description

An existing iOS app still uses a SceneKit product viewer built around
`SCNView`, `SCNScene`, and `SCNNode`. The next content drop includes
`hero.usdz`, several OBJ files from the art team, and a plan that says:

- load `hero.usdz` directly with `SCNScene(url:)`;
- keep new app-facing models as OBJ because the artists already export OBJ;
- defer any renderer or asset-pipeline migration until later.

Review the plan and correct the SceneKit loading guidance. Explain where the
handoff boundary should be if the team wants USD/USDZ as the long-term asset
pipeline.

## Output Specification

Create a file named `scenekit-asset-loading-review.md` containing:

- a short verdict on the proposed loading plan;
- corrected SceneKit asset-loading guidance and a small Swift snippet;
- a brief handoff section for RealityKit or migration work;
- any review notes about current SceneKit project scope.

Do not create an Xcode project or convert assets.
