# Calendar Booking Access Review

## Problem/Feature Description

A booking app is adding calendar integration for iOS 26. The current proposal is to keep the old calendar usage string, ask for calendar permission with the older EventKit request method, request write-only access for privacy, and then scan the user's calendar to avoid booking conflicts before saving an event.

The product also wants a separate Add to Calendar button where the user can review and adjust the event in the system-provided calendar sheet before saving.

## Output Specification

Write a concise engineering review in `answer.md`. Explain what should change, which privacy/access model fits each product behavior, and include Swift API names or snippets where they make the correction clearer.
