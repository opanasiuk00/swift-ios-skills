Review this Core Data data-flow plan:

- The main app and widget share a SQLite store.
- Imports use batch inserts on a background context.
- Cleanup uses batch deletes.
- The UI assumes `viewContext` will notice those SQL-level changes automatically.
- The team does not store persistent history tokens.
- Managed objects are passed directly into detached tasks for background edits.

Explain what needs to change and why.
