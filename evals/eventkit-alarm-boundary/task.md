# Calendar Alert Architecture Review

## Problem/Feature Description

A teammate proposes using the app's notification service for every calendar alert. Their idea is to store only basic event and reminder fields in Calendar/Reminders, then mirror all alert timing in app-owned local or remote notifications.

Review the architecture and explain how to divide responsibilities between native calendar/reminder data and app-owned notification workflows.

## Output Specification

Write `answer.md` as a concise architecture review. Include examples of the right API family for native calendar/reminder alerts and identify the cases that should remain in the app notification layer.
