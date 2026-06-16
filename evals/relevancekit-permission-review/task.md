# RelevanceKit Permission Review

## Problem/Feature Description

Review this RelevanceKit plan for a watchOS 26 widget:

- Add `NSLocationWhenInUseUsageDescription` only to the widget extension.
- Request one broad HealthKit permission for all fitness relevance clues.
- Create `RelevantContext.location(category: .cafe)!`.
- Use `.fitness(.activityRingsIncomplete)`.
- Assume the same RelevanceKit clues will improve an iPhone Smart Stack.

Fix the plan and show corrected snippets where useful.

## Output Specification

Create a file named `relevancekit-permission-review.md` containing:

- Correct app-versus-widget location setup.
- Widget location authorization checks.
- Optional handling for point-of-interest category relevance.
- Exact HealthKit read types for the fitness clues.
- The watchOS-only effect boundary for RelevanceKit.
