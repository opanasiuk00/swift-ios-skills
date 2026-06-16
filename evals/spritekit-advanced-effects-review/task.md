# SpriteKit Advanced Effects Plan Review

## Problem/Feature Description

A team proposes the following SpriteKit effects plan for an iOS 26 game:

- Wrap `SKTextureAtlas.preloadTextureAtlases` in `withCheckedContinuation`.
- Document `u_sprite_size` as a SpriteKit built-in shader variable.
- Allocate a new `SKShader` for each enemy every time one spawns.
- Remove physics bodies and nodes directly inside `didBegin(_:)` as soon as a contact happens.

Review the plan and correct it for current SpriteKit guidance.

## Output Specification

Create a file named `spritekit-effects-plan-review.md` containing:

- Corrected texture atlas preload guidance.
- A shader built-in symbol correction, including how to handle sprite size if needed.
- Shader lifecycle and reuse guidance.
- Physics contact mutation guidance.
- A short list of the original plan's concrete risks.
