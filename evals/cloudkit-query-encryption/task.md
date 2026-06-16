# CloudKit Query and Encryption Review

## Problem/Feature Description

A privacy review found a CloudKit profile feature that mixes searchable profile
data, private notes, and uploaded avatars. The team wants one record type to work
for public discovery and for a signed-in user's private profile details.

Their draft stores private profile notes with `record.encryptedValues`, runs a
public-database query that filters and sorts on that same field, reuses an
already-deployed field name for the encrypted value, searches note titles with a
`title CONTAINS` predicate, and stores avatars as `CKAsset`.

Review the plan and explain how to split or adjust the record fields and queries.

## Output Specification

Create `cloudkit-query-encryption-review.md` containing:

- A concise review of the data-placement and query mistakes.
- Corrected guidance for encrypted fields, searchable fields, and assets.
- Example predicate guidance for prefix or full-text search.
- A short migration note for already-deployed fields.
