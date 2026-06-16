# Swift Codable SwiftData and AppStorage Boundary Review

## Problem/Feature Description

A storage plan uses a SwiftData `@Model` with an optional `Address` struct that conforms to `Codable`, and a SwiftUI settings screen stores a `UserPreferences` struct in `@AppStorage`. The draft says Codable value types only work in SwiftData on iOS 18+ and proposes transformable/blob workarounds. It also says synthesized `Codable` defaults are enough when the stored preferences JSON is `{}`.

## Output Specification

Create `swift-codable-storage-boundary-review.md` with corrected, source-grounded Codable guidance. State clearly that SwiftData persists compatible noncomputed stored properties declared on `@Model` types, including `Codable` structs and enums when they are part of the durable model schema. Include small Swift snippets only where they clarify SwiftData value-type compatibility, direct `@AppStorage` use with a `RawRepresentable` JSON `String` raw value, or missing-key defaults. A complete `RawRepresentable` wrapper with `init?(rawValue:)` and `rawValue` that self-encodes/decodes the Codable preference as a JSON string is the expected bridge. Do not propose `@Attribute(.transformable)`, encoded `Data`, or encoded `String` blob storage as a fallback. Keep detailed SwiftData schema design and SwiftUI state management out of scope.
