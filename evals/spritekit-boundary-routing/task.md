# SpriteKit Game Architecture Boundaries

## Problem/Feature Description

An iOS game team wants one architecture note that covers:

- SpriteKit gameplay rendering.
- Game Center sign-in, leaderboards, achievements, matchmaking, saved games, and player identity.
- SceneKit or RealityKit 3D cutscenes.
- TabletopKit-style board rules, pieces, cards, dice, and spatial table sessions.
- SharePlay voice chat and synchronized group sessions.

Explain what belongs in SpriteKit and what should be handed to sibling framework guidance.

## Output Specification

Create a file named `spritekit-boundary-architecture.md` containing:

- A clear SpriteKit ownership section.
- A sibling-framework handoff section for GameKit, SceneKit or RealityKit, TabletopKit, and SharePlay or GroupActivities.
- Any narrow SpriteKit integration boundaries that are relevant, without expanding SpriteKit into those sibling domains.
