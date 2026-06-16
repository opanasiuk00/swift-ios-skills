# Publisher App Custom Ad Attribution Review

## Problem/Feature Description

A publisher app team is replacing a generic ad SDK integration with a custom-rendered app-install card. The ad network will provide a signed impression blob, and the publisher app needs a review-ready implementation note that explains how to turn that blob into an attributable impression, how the tappable ad view should be wired, and how the app should recover when an ad card remains onscreen for a while before the user taps it.

The team also uses StoreKit-rendered promotion surfaces in another part of the app, so the note should keep the custom-rendered flow separate from the StoreKit-rendered flow instead of treating every ad surface the same way.

## Output Specification

Create a file named `adattributionkit-click-through.md` containing:

- a concise publisher-app implementation outline;
- Swift snippets where helpful;
- a short review checklist for the implementation; and
- a short distinction between custom-rendered and StoreKit-rendered ad handling.
