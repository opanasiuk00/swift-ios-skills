# SwiftData CloudKit Schema Review

## Problem/Feature Description

A team is preparing a SwiftData store for iCloud sync. A reviewer proposed
making every model property optional, but the current schema also contains
uniqueness, a required owner relationship, a restrictive delete rule, and a
large image blob.

```swift
@Model
final class Profile {
    @Attribute(.unique) var email: String
    var displayName: String
    var avatarData: Data
    @Relationship(deleteRule: .deny, inverse: \Owner.profiles)
    var owner: Owner

    init(email: String, displayName: String, avatarData: Data, owner: Owner) {
        self.email = email
        self.displayName = displayName
        self.avatarData = avatarData
        self.owner = owner
    }
}
```

Review the schema and produce practical correction guidance for iOS 26 without
overcorrecting parts that are already compatible.

## Output Specification

Create `swiftdata-cloudkit-schema-review.md` containing:

- A concise list of incompatible schema choices.
- A corrected model sketch.
- Notes on schema rollout and production CloudKit concerns.
- A short answer to the claim that every scalar property must be optional.
