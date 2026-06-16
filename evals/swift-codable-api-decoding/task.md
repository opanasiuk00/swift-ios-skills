# Swift Codable API Decoding Review

## Problem/Feature Description

An iOS team built API response models and decoding code with several issues: every response type conforms to `Codable`, JSON is decoded before HTTP status is checked, ISO 8601 date strings are decoded with a default `JSONDecoder`, `image_url` is expected to fill an `imageURL` property through `.convertFromSnakeCase`, and a generic response envelope is decoded using a `decoder` variable outside the scope where it was declared.

## Output Specification

Create `swift-codable-api-decoding-review.md` with concise corrected guidance and Swift snippets where they clarify the model shape, decoder setup, response validation, key mapping, or envelope decoding. Explicitly correct every read-only API response model to `Decodable`, not `Codable`, and say `Codable` is only for types that also need encoding. State definitively that `.convertFromSnakeCase` maps `image_url` to `imageUrl`, not `imageURL`, so `imageURL` needs `CodingKeys`. Also call out that the envelope decoder must be configured in the helper because a decoder declared in another function is out of scope. Keep networking architecture details at the boundary and do not turn the answer into a full API client design guide.
