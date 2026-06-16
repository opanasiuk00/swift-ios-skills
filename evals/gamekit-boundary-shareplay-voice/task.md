# GameKit Boundary and Voice Architecture

## Problem/Feature Description

A team wants one iOS game architecture note covering:

- Game Center authentication and restrictions,
- leaderboards, achievements, real-time and turn-based multiplayer,
- SpriteKit gameplay rendering,
- SceneKit 3D board scenes,
- TabletopKit board rules,
- SharePlay party chat,
- and old GameKit voice chat maintenance.

They need to know what belongs in GameKit and what should be handed to sibling
framework guidance.

## Output Specification

Create a file named `gamekit-boundary-voice.md` containing:

- A framework-boundary map for GameKit versus SpriteKit, SceneKit,
  TabletopKit, and GroupActivities/SharePlay.
- A concise GameKit implementation checklist for authentication, restrictions,
  leaderboards, achievements, matchmaking, match data, saved games, challenges,
  and identity verification.
- Guidance for new social audio versus legacy `GKVoiceChat` maintenance.
- A short networking-data safety note for real-time matches.

Do not create an Xcode project. Keep the answer as architecture guidance and
focused snippets only.
