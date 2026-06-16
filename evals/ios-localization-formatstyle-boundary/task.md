# FormatStyle Ownership Boundary

## Problem/Feature Description

A team is not adding new languages yet. They need to design a custom `ParseableFormatStyle` for follower counts like `12.5K`, audit `Date.IntervalFormatStyle` usage, and format URLs for display.

They want to know whether the iOS localization skill should own that work or whether it belongs to another skill/domain.

## Output Specification

Create `formatstyle-routing.md` with a short routing answer. Include only the minimum localization advice that still matters, and do not produce a full custom `FormatStyle` implementation.
