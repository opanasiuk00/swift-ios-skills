# Journal App Backend Routing

## Problem

A journaling app needs private short summaries on recent Apple operating systems, a possible local open-source model fallback on some devices, and a custom sentiment classifier that the team already trained. Product wants a single architecture note explaining which on-device AI stack belongs to each responsibility and where adjacent framework details should be handed off.

Write the architecture note for the team. It should help the app choose the right backend for each feature, avoid mixing custom classifier deployment with prompt-based generation, and preserve clean boundaries with sibling framework guidance. Include review notes for memory and lifecycle behavior, device validation, privacy fallback boundaries, and sibling handoffs.

## Output

Create a Markdown file named `journal-ai-backend-routing.md`.
