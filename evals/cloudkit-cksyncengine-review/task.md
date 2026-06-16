# CloudKit Sync Engine Review

## Problem/Feature Description

An iOS team is replacing a hand-written CloudKit sync loop with a new `CKSyncEngine`
manager for a notes app. Their draft wires the engine to the app-wide database,
expects every edit to upload immediately, and keeps the existing app capabilities
unchanged because CloudKit subscriptions already deliver notifications.

The draft also includes this delegate shape:

```swift
final class NotesSyncManager: CKSyncEngineDelegate {
    let syncEngine: CKSyncEngine

    init(container: CKContainer = .default()) {
        let config = CKSyncEngine.Configuration(
            database: container.publicCloudDatabase,
            stateSerialization: nil,
            delegate: self
        )
        syncEngine = CKSyncEngine(config)
    }

    func handleEvent(_ event: CKSyncEngine.Event, syncEngine: CKSyncEngine) {
        // update local cache
    }

    func nextRecordZoneChangeBatch(
        _ context: CKSyncEngine.SendChangesContext,
        syncEngine: CKSyncEngine
    ) -> CKSyncEngine.RecordZoneChangeBatch? {
        CKSyncEngine.RecordZoneChangeBatch(
            pendingChanges: Array(syncEngine.state.pendingRecordZoneChanges)
        ) { id in recordFor(id: id) }
    }
}
```

Review the plan for iOS 26 and produce corrected implementation guidance.

## Output Specification

Create `cloudkit-sync-engine-review.md` containing:

- A concise review of what is wrong with the proposal.
- Corrected Swift snippets for the manager shape where useful.
- Required project capability and persistence notes.
- A short note on when manual sync calls are appropriate.
