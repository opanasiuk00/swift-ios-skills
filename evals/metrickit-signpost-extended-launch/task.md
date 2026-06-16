# MetricKit Signpost And Extended Launch Correction

## Problem/Feature Description

A code review found this draft guidance in a MetricKit setup note:

```swift
let log = MXMetricManager.makeLogHandle(category: "network")
let signpostID = MXSignpostIntervalData.makeSignpostID(log: log)
mxSignpost(.begin, log: log, name: "DataFetch", signpostID: signpostID)
// work
mxSignpost(.end, log: log, name: "DataFetch", signpostID: signpostID)

let taskID = MXLaunchTaskID("com.example.restore")
MXMetricManager.shared.extendLaunchMeasurement(forTaskID: taskID)
restoreStateOnBackgroundQueue()
MXMetricManager.shared.finishExtendedLaunchMeasurement(forTaskID: taskID)
```

## Output Specification

Create `metrickit-api-corrections.md` explaining what is wrong and showing the corrected MetricKit guidance. Use MetricKit APIs rather than OSLog signpost substitutes. The corrected signpost sample must not allocate or pass any signpost ID; show `mxSignpost(.begin, log:name:)` and `mxSignpost(.end, log:name:)` with the advanced parameters left at their defaults. Name where custom MetricKit signpost metrics appear. In the extended launch section, explicitly mention main-thread calls, early state-restoration or first-scene-active timing, overlapping task windows, the maximum 16-task limit, and finishing every started task.
