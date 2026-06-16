# Network Framework, ATS, and Security Boundary Review

## Problem/Feature Description

An iOS 26 team proposes using Network.framework for all REST API calls to avoid App Transport Security, setting `NSAllowsArbitraryLoads` globally, implementing certificate pinning by hashing bytes from `SecKeyCopyExternalRepresentation`, and wrapping `NWPathMonitor` in a custom `AsyncStream` helper.

## Output Specification

Create `network-framework-ats-security-review.md` with a concise correction-focused review. Explain when URLSession, Network.framework, ATS exceptions, certificate-trust guidance, `NWPathMonitor`, and iOS 26 `NetworkConnection` each apply. Preserve the boundary with the security skill.
