# Memory, Hang, and Thread Sanitizer Corrections

## Problem/Feature Description

Review this debugging plan for an iOS app:

- Use the Leaks template to prove every retain cycle.
- Run `leaks --atExit -- ./MyApp.app/MyApp` for the iOS build.
- Treat any 250 ms main-thread pause as a severe hang.
- Enable Thread Sanitizer on a real iPhone test run.

## Output Specification

Create `memory-hang-tsan-corrections.md` with corrected guidance. Keep the answer focused on local debugging and Instruments/Xcode diagnostics; do not implement a MetricKit telemetry pipeline.
