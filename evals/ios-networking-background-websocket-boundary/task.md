# Background Transfer and WebSocket Boundary Review

## Problem/Feature Description

An iOS team wants a single networking manager that uses a background `URLSession` for JSON polling, large file downloads, file uploads created from in-memory `Data`, and a chat `URLSessionWebSocketTask` that should keep receiving after the user force-quits the app.

## Output Specification

Create `background-websocket-boundary-review.md` with a concise review of what should change. Include the background transfer constraints, app lifecycle limits, and WebSocket boundary. Do not redesign the chat product or notification UI.
