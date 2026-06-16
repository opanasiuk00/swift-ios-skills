# Drawing Architecture Boundary

## Problem/Feature Description

A PDF sketching app already has years of PencilKit code for custom brush behavior, raw stroke analytics, and lasso-centric editing workflows. Product now wants nicer review annotations: callout boxes, arrows, labels, and image stamps over rendered PDF pages.

Write the architecture recommendation for whether the team should replace the current drawing canvas, layer a new framework beside it, or keep the old system untouched.

## Output Specification

Create a file named `paperkit-pencilkit-boundary.md` containing:

- A recommendation for which framework owns each part of the experience.
- A migration or coexistence path for existing drawings.
- Notes about PDF/page background content and app configuration.
