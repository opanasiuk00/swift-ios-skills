# MetricKit Telemetry Setup Review

## Problem/Feature Description

An iOS team plans to add MetricKit telemetry, but their draft has the subscriber created inside a SwiftUI dashboard view, implements only `didReceive(_ payloads: [MXMetricPayload])`, parses and uploads payloads before saving them, and ignores reports that may have arrived before the dashboard opens.

## Output Specification

Create `metrickit-telemetry-plan.md` with corrected guidance and a concise Swift sketch where useful. Show the subscriber callback persisting raw payload JSON and then enqueueing out-of-band work; do not parse or upload from the callback itself. Mention the daily/non-immediate cadence of metric payloads. Focus on production ingestion behavior and avoid turning this into an Instruments tutorial.
