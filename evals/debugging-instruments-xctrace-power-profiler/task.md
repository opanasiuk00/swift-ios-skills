# xctrace and Power Profiler Plan

## Problem/Feature Description

A team has an iOS app with a slow feed refresh and battery-drain complaints. They also want CI to collect a Time Profiler trace using `xctrace`, and sometimes add Allocations to that same recording.

## Output Specification

Create `xctrace-power-profiler-plan.md` with a concise profiling plan. Include the Instruments templates or instruments to use for the symptoms, mention the expected device/build setup, and show the `xcrun xctrace record` command shape for both a basic Time Profiler launch and a Time Profiler recording that adds Allocations.
