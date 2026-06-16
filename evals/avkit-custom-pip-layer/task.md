# Custom AVPlayerLayer Picture in Picture

## Problem/Feature Description

The product team wants a custom iOS video player surface instead of `AVPlayerViewController`, but it still needs a Picture in Picture button. The player renders with `AVPlayerLayer`.

Design implementation snippets for the custom player and PiP control.

## Output Specification

Create a file named `custom-pip-layer.md` containing:

- An `AVPlayerLayer`-backed view or equivalent content source.
- PiP controller setup and lifecycle/delegate handling.
- Button-state logic for current PiP availability.
- Audio/background setup notes needed for PiP.
- A short review checklist for the custom PiP integration.
