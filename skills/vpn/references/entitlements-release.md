# Entitlements and Release Review

Use this reference for capabilities, provisioning, bundle IDs, and archive
checks for VPN apps.

## Contents

- [Required Targets](#required-targets)
- [Capabilities](#capabilities)
- [Bundle Identifiers](#bundle-identifiers)
- [Archive Checks](#archive-checks)
- [App Review Notes](#app-review-notes)

## Required Targets

A production packet tunnel VPN usually has:

- Main app target: user UI, account/session state, VPN profile install/control.
- Packet Tunnel extension target: protocol connection and packet tunnel.
- Shared framework/package modules: profile parsing, config validation, logging,
  domain models, and services safe for both processes.

Do not put UIKit or app-only dependencies into modules linked by the extension.

## Capabilities

Both main app and extension need matching capability setup where applicable:

- Network Extensions with Packet Tunnel provider entitlement.
- App Groups for shared diagnostics or config references.
- Keychain Sharing when credentials are read by both host and extension.
- Background modes only when the product has a specific supported need.

Packet Tunnel entitlements require the Apple Developer account to have the
capability enabled for the App IDs. A local build setting alone is not enough.

## Bundle Identifiers

Keep bundle IDs stable:

```text
com.example.vpn
com.example.vpn.PacketTunnel
```

The host app's `NETunnelProviderProtocol.providerBundleIdentifier` must exactly
match the extension bundle ID. If this changes, remove stale installed VPN
profiles before retesting.

## Archive Checks

Before release:

- Archive with the same provisioning profiles used for distribution.
- Inspect the `.appex` for disallowed nested `Frameworks` folders if the build
  setup or TunnelKit fork creates them.
- Confirm all embedded frameworks are extension-safe.
- Confirm no server profiles, debug certs, sample keys, or `.ovpn` fixtures are
  copied into the app bundle by mistake.
- Confirm debug logging is disabled or masks private data.
- Confirm NetworkExtension capability is present in the signed app and extension
  entitlements.

## App Review Notes

VPN apps often need clear review notes:

- Explain the VPN purpose and account requirements.
- Provide a demo account or test server if login is required.
- Explain any on-demand or include-all-networks behavior.
- Document why VPN entitlement is required.
- Keep privacy labels consistent with traffic handling, diagnostics, analytics,
  account data, and server selection.
