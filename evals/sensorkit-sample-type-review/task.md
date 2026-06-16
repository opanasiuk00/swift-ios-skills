# SensorKit Fetch Handler Review

## Problem/Feature Description

A research app has a shared `SRSensorReaderDelegate` that casts fetched samples
based on `reader.sensor`. The draft casts accelerometer data to
`CMAccelerometerData`, rotation rate to `CMGyroData`, wrist temperature directly
to `SRWristTemperature`, ECG to `SRElectrocardiogramSample`, and PPG to
`SRPhotoplethysmogramSample`. It also handles successful fetch results but does
not define a complete callback strategy for recording, device discovery, and
fetch failures.

## Output Specification

Create `sensorkit-fetch-handler-review.md` with the corrected sample shapes and
a delegate callback checklist. Keep the output focused on SensorKit fetch
handling rather than building a full app.
