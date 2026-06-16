# Focus Bug Scope Review

## Problem/Feature Description

An iPad app team filed a broad "focus is broken" ticket against their accessibility work. In the same screen, VoiceOver lands nowhere useful after a custom modal closes, several visible actions have duplicate names when using voice commands, a custom card is skipped during hardware-keyboard navigation, arrow-key movement between side-by-side panels feels wrong, and the tvOS build needs routing across an empty gap between controls.

The team needs a concise scope review that separates immediate accessibility fixes from focus-engine implementation work so the right people can take the next steps.

## Output Specification

Write `focus-scope-review.md`. Include what the accessibility workstream should fix first, including accessibility focus restoration, modal accessibility behavior, unique Voice Control names, and `accessibilityInputLabels`; what should be handed to the focus-engine workstream; why the distinction matters; and how accessibility element order/grouping affects VoiceOver swipe order, Switch Control scan order, Voice Control overlay targeting, and Full Keyboard Access reachability review.
