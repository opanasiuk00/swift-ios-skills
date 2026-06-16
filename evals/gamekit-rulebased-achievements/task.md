# GameKit Rule-Based Matchmaking and Challenges

## Problem/Feature Description

An iOS game needs advanced Game Center features:

- rule-based matchmaking with a competitive queue,
- request properties for skill and region,
- recipient properties for invited players,
- fallback role matching using `playerAttributes`,
- achievement progress updates,
- and challenge compose UI for friends.

The team is worried that older examples may still compile poorly or encode
wrong matchmaking assumptions.

## Output Specification

Create a file named `gamekit-matchmaking-achievements.md` containing:

- A Swift-oriented implementation outline for the matchmaking request.
- Availability and value-format caveats for queues and matchmaking properties.
- A concise explanation of when to use matchmaking rules versus player groups
  and attributes.
- Correct achievement progress and challenge compose snippets.
- A short review checklist for App Store Connect and Game Center setup risks.

Do not create an Xcode project. Keep the answer as implementation guidance and
snippets only.
