# Migration Plan Risk Review

## Problem/Feature Description

An engineering lead drafted an AppMigrationKit plan for a large notes app. The draft says the import progress property can create a new progress object whenever it is read, export should first convert the app database to a temporary JSON package, archiver cancellation should be caught so it can be logged, and shared group data can be written during import because the system will clean up on failure.

The lead wants a direct technical review that corrects risky assumptions before implementation starts. The answer should focus on what to change and why, with small snippets only when they make the corrected approach clearer.

## Output Specification

Create `migration-plan-review.md` with a correction-focused review of the plan.
