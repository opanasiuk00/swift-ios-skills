# Core ML Prediction Service API Review

## Problem

A Swift team is building an iOS 26 Core ML prediction service. Their draft loads a compiled model with `MLModel(contentsOf:)`, calls `try await model.prediction(from:)` for ordinary stateless inference, uses `model.predictions(from: batchProvider)` for a no-options batch path, and documents "async prediction is available on iOS 17."

Review the draft and provide corrected Swift snippets and availability notes. Keep the answer focused on Swift Core ML integration; do not turn it into Python conversion, quantization, or framework-selection guidance.

## Output

Create a Markdown file named `coreml-api-corrections.md`.
