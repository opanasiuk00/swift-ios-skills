# Document Migration Setup Review

## Problem/Feature Description

A document editor team is preparing a migration path for users who buy a new iPhone after using the Android version of the app for years. The Android app can provide a directory of user documents and metadata during device setup. The iOS team needs a concise implementation brief for the iOS side before they create the migration target.

The brief should cover the shape of the extension, how it participates in import and optional export, what entitlement and platform availability details the project owner needs to know, how the extension reaches the containing app's files, and what the installed app should do when it launches after migration.

## Output Specification

Create `document-migration-setup.md` with a source-grounded setup brief. Include Swift or entitlement snippets only where they make the setup unambiguous.
