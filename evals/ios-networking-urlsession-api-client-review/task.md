# URLSession API Client Review

## Problem/Feature Description

An iOS team built a Swift API client where every request uses `URLSession.shared.data(for:)`, decodes JSON before checking HTTP status, retries all thrown errors including cancellation and every 4xx response, adds bearer tokens inline in each request, stores those tokens in `UserDefaults`, and tests only by mocking the client protocol.

## Output Specification

Create `urlsession-api-client-review.md` with a concise correction-focused review. Include Swift snippets where they clarify response validation, retry policy, request middleware, or transport-level testing. Keep credential-storage details at the boundary and do not turn the answer into a full Keychain implementation guide.
