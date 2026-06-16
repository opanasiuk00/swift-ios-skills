# Alternative Browser Engine Setup Review

## Problem/Feature Description

An iOS browser team is preparing an alternative browser engine build. The host app currently has only `com.apple.developer.web-browser-engine.host`, the three helper targets are generic extensions without type-specific BrowserEngineKit entitlements, the app has no `UIRequiredDeviceCapabilities` entry, and a tab starts web content work before networking and rendering endpoints are connected.

Write a concise setup review that corrects the entitlement, Info.plist/build-setting, eligibility, and process-bootstrap problems for a BrowserEngineKit app.

## Output Specification

Create `browserenginekit-setup-review.md` with:

- Required host and extension entitlements.
- Required device capability and `arm64e` distribution guidance.
- Device eligibility guidance.
- The correct host-brokered XPC bootstrap sequence.
- Boundaries that avoid replacing BrowserEngineKit with WebKit for an alternative engine.
