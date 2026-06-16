# Swift Codable Key Strategy Initialisms

## Problem/Feature Description

A teammate wants to delete every `CodingKeys` enum because the decoder uses `.convertFromSnakeCase`. The payload includes keys such as `display_name`, `avatar_url`, `base_uri`, and `user_id`, while the Swift model uses names such as `displayName`, `avatarURL`, `baseURI`, and `userID`.

## Output Specification

Create `swift-codable-key-strategy-review.md` with a concise recommendation and a corrected Swift model. Preserve automatic key strategies where they are appropriate, but handle names that need exact Swift initialism spelling.
