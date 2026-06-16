Review this Core Data migration plan for an iOS 26 app:

- The app has three model versions.
- The team creates `NSLightweightMigrationStage(["ModelV1", "ModelV2"])`.
- The custom stage creates `NSManagedObjectModelReference(named: "ModelV2", in: .main)`.
- The migration manager is created but not attached to the persistent store configuration.

Give concise corrected guidance with Swift snippets where useful.
