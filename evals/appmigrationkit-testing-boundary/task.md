# Round-Trip Test and Manual QA Plan

## Problem/Feature Description

The QA team for a file-based iOS app wants confidence that the upcoming AppMigrationKit support can round-trip documents and metadata. Product also asked whether the shipping app can include a hidden menu item that starts a real migration session for support staff.

Prepare a test and manual QA plan that keeps production boundaries clear. The plan should show how unit tests can exercise the migration logic and what kinds of manual validation or debug-only affordances are acceptable without giving users or support staff a misleading production trigger.

## Output Specification

Create `migration-testing-plan.md` with the recommended automated test flow, manual QA guidance, and a short "must not ship" section.
