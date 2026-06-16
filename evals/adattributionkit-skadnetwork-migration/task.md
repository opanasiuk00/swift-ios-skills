# Attribution Migration Guidance

## Problem/Feature Description

A mobile growth team has a draft migration plan for a campaign-measurement integration. The draft says the newer attribution framework fully replaces the older StoreKit-based attribution path, so the app can remove old update calls and simplify publisher configuration to a single identifier family. Before this guidance goes into an engineering ticket, they need a correction note that explains what should stay, what should change, and how dual-framework apps should behave during migration.

The note should be written for iOS engineers who already know the business goal but need precise technical boundaries so they do not accidentally lose attribution data while migrating.

## Output Specification

Create a file named `adattributionkit-migration-review.md` containing:

- a corrected migration recommendation;
- a table of incorrect draft assumptions and corrected guidance;
- the expected conversion-update approach for apps using one framework versus both frameworks; and
- a publisher-app configuration note for identifier compatibility.
