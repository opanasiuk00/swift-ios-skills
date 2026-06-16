# Vision Transformer Conversion Review

## Problem

An ML engineer drafted a conversion plan for a vision transformer that was trained in PyTorch. The plan exports the model directly from the training notebook, converts to an older Core ML file format, allows broad image-size ranges, compresses aggressively before a baseline is measured, and assumes the profiling API is available on every iOS 17 device. The product targets iPhone 15 Pro and an M4 iPad.

Review the plan and replace it with a safer handoff checklist for conversion, optimization, validation, and profiling. Stay focused on the Python-side conversion and optimization work; do not turn this into a full Swift app integration guide.

## Output

Create a Markdown file named `coreml-conversion-review.md`.
