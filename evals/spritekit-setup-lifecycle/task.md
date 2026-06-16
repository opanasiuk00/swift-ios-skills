# SpriteKit Mini-Game Setup Note

## Problem/Feature Description

An iOS team is building a SwiftUI-hosted 2D arcade mini-game for iOS 26. The game needs an `SKScene` with player and enemy sprites, contact-based hit handling, a camera-following world with a HUD, and texture atlas preloading before gameplay starts.

Write a concise implementation note that corrects common setup mistakes and gives snippets the team can adapt.

## Output Specification

Create a file named `spritekit-mini-game-setup.md` containing:

- A SwiftUI `SpriteView` integration snippet that avoids recreating the scene during `body` updates.
- An `SKScene` setup snippet showing lifecycle placement, scale mode, physics contact delegate, and distinct physics masks.
- Contact-handling guidance that avoids mutating the physics world during contact callbacks.
- Camera/HUD guidance using SpriteKit camera nodes.
- Texture atlas preload guidance using current SpriteKit async APIs where async Swift code is shown.
