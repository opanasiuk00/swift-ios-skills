# GameKit Identity and Saved Games Review

## Problem/Feature Description

A game team has an iOS 26+ GameKit plan with several stale assumptions:

```swift
let (publicKeyURL, signature, salt, timestamp) =
    try await GKLocalPlayer.local.fetchItems(forIdentityVerificationSignature: nil)
let playerID = GKLocalPlayer.local.playerID
sendToServer(publicKeyURL, signature, salt, timestamp, playerID)

let saves = try await GKLocalPlayer.local.fetchSavedGames() ?? []

if turnData.count < 64 * 1024 {
    try await match.endTurn(withNextParticipants: next, turnTimeout: GKTurnTimeoutDefault, match: turnData)
}
```

The team also wants multiple save slots with the same save name because they
expect Game Center to return separate entries for each device.

## Output Specification

Create a file named `gamekit-identity-saves-review.md` containing:

- A correction-focused review of the identity verification flow, including what
  the client should send and what the server should verify.
- A saved-game section covering prerequisites and how same-name saves behave.
- A Swift-oriented note for checking GameKit object-reported match data limits.
- A short "do not ship" checklist for the stale assumptions in the snippet.

Do not create an Xcode project or backend service. Keep the answer as guidance
and focused snippets only.
