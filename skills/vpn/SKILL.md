---
name: vpn
description: Build, review, debug, or improve iOS/macOS VPN apps using NetworkExtension packet tunnel providers, NETunnelProviderManager, NETunnelProviderProtocol, NEPacketTunnelProvider, TunnelKit, OpenVPN, WireGuard, App Groups, Keychain Sharing, Packet Tunnel entitlements, providerConfiguration, save/load preferences, start/stop lifecycle, on-demand rules, kill switch settings, packet flow, tunnel network settings, and extension logging.
---

# VPN

Use this skill for Apple-platform VPN work: host app configuration, packet
tunnel app extensions, NetworkExtension preferences, TunnelKit integration,
OpenVPN/WireGuard provider configs, entitlements, lifecycle debugging, and
App Store/release readiness.

Default to iOS 15+ and Swift concurrency examples when the deployment target is
unknown. Treat the VPN as two processes: the host app installs and controls a
VPN profile; the packet tunnel extension owns protocol connection, packet I/O,
network settings, and tunnel teardown.

## Contents

- [Workflow](#workflow)
- [Reference Loading](#reference-loading)
- [Architecture Boundaries](#architecture-boundaries)
- [Core NetworkExtension Flow](#core-networkextension-flow)
- [TunnelKit Flow](#tunnelkit-flow)
- [Review Checklist](#review-checklist)
- [Common Mistakes](#common-mistakes)
- [References](#references)

## Workflow

1. Classify the task: app installation/control, packet tunnel extension,
   TunnelKit protocol integration, config parsing, entitlements, diagnostics,
   or release review.
2. Load only the matching reference files from [Reference Loading](#reference-loading).
3. Identify the boundary being changed: host app, extension, shared app group,
   keychain, server config, or build settings.
4. Preserve the process boundary. Do not move packet I/O into the host app or
   UI/profile installation into the extension.
5. Verify with a real device plan. Packet Tunnel entitlements and VPN prompts
   cannot be fully validated on a simulator-only path.

## Reference Loading

| If the task involves | Load |
| --- | --- |
| Raw NetworkExtension setup, profile install, connect/disconnect, status | [networkextension.md](references/networkextension.md) |
| TunnelKit, OpenVPN, WireGuard, `NetworkExtensionVPN`, provider configs | [tunnelkit.md](references/tunnelkit.md) |
| Packet tunnel extension lifecycle, `startTunnel`, `stopTunnel`, network settings, packet flow | [packet-tunnel-provider.md](references/packet-tunnel-provider.md) |
| Entitlements, App Groups, Keychain Sharing, extension bundle IDs, release/archive checks | [entitlements-release.md](references/entitlements-release.md) |
| VPN status bugs, install prompts, provider crashes, logs, data counters | [debugging.md](references/debugging.md) |
| Full VPN review | Load all references, then apply the [Review Checklist](#review-checklist) |

## Architecture Boundaries

- Host app: builds `NETunnelProviderProtocol`, saves preferences, starts and
  stops the tunnel, observes VPN status, and owns user-facing account/server UI.
- Packet tunnel extension: subclasses `NEPacketTunnelProvider` or a TunnelKit
  provider, reads `providerConfiguration`, establishes the protocol session,
  calls `setTunnelNetworkSettings`, and handles packet I/O.
- App Group: shares diagnostics, last error, data counters, debug logs, and
  non-secret state between host app and extension.
- Keychain: stores passwords, private keys, tokens, and certificate identities.
  Use persistent references when `NETunnelProviderProtocol` needs credentials.
- Server config model: represents OpenVPN or WireGuard parameters without
  UIKit, view models, or profile installation logic.

## Core NetworkExtension Flow

Use this sequence for custom packet tunnels:

```swift
let manager = NETunnelProviderManager()
let proto = NETunnelProviderProtocol()
proto.providerBundleIdentifier = "com.example.app.PacketTunnel"
proto.serverAddress = "vpn.example.com"
proto.providerConfiguration = [
    "profileID": profile.id,
    "transport": "wireguard"
]
proto.passwordReference = passwordPersistentReference

manager.localizedDescription = profile.displayName
manager.protocolConfiguration = proto
manager.isEnabled = true

try await manager.saveToPreferences()
try await manager.loadFromPreferences()
try manager.connection.startVPNTunnel()
```

Always save and then reload before starting. The reloaded manager is the system
source of truth for the profile the user approved.

## TunnelKit Flow

For TunnelKit-based apps, prefer its host-app wrapper instead of hand-rolling
the same manager lifecycle repeatedly:

```swift
let vpn = NetworkExtensionVPN()
await vpn.prepare()
try await vpn.install(
    "com.example.app.PacketTunnel",
    configuration: providerConfiguration,
    extra: extra
)
try await vpn.reconnect(after: .milliseconds(300))
```

Use TunnelKit provider configuration types to serialize OpenVPN or WireGuard
configuration into `NETunnelProviderProtocol.providerConfiguration`. Keep
OpenVPN and WireGuard construction in server/profile services, not in view
controllers.

## Review Checklist

- The host app and packet tunnel extension both have Packet Tunnel
  NetworkExtension entitlements for their bundle IDs.
- App Groups and Keychain Sharing are enabled on every target that reads shared
  state or credentials.
- The host app calls `saveToPreferences()` and then `loadFromPreferences()`
  before starting a newly installed or updated tunnel.
- `providerBundleIdentifier` matches the packet tunnel extension bundle ID.
- `providerConfiguration` contains only serializable configuration values and
  no raw secrets.
- Secrets are stored in Keychain, not `UserDefaults`, `.ovpn` temp files, logs,
  or `providerConfiguration`.
- The extension calls `setTunnelNetworkSettings` before completing a successful
  `startTunnel` path.
- `stopTunnel(with:completionHandler:)` or provider-specific teardown always
  calls its completion handler.
- VPN status is observed through `NEVPNStatusDidChange` and handled as an
  async state machine, not as a synchronous connect result.
- On-demand rules and kill-switch settings are explicit and tested on device.
- OpenVPN compression, cipher, TLS wrapping, routes, and server-pushed options
  match the server profile.
- WireGuard keys, allowed IPs, endpoint, DNS, MTU, and default gateway behavior
  match the server profile.
- Extension logs mask private data by default.
- Release/archive checks account for extension embedding, unsupported
  frameworks in `.appex`, and required App Store capability approval.

## Common Mistakes

- Starting a tunnel from the manager instance saved before preferences reload.
- Putting passwords, private keys, or full `.ovpn` blobs into
  `providerConfiguration`.
- Testing only on simulator and missing entitlement/profile failures.
- Forgetting that the extension is a separate process with its own container,
  memory pressure, logs, and lifecycle.
- Calling the `startTunnel` completion handler before network settings are set.
- Leaving stale VPN profiles installed after changing the extension bundle ID.
- Treating `.invalid` and `.disconnected` VPN status as the same diagnostic
  cause.
- Enabling kill switch or include-all-networks without testing local network,
  captive portal, and reconnect behavior.
- Letting UIKit controllers construct OpenVPN/WireGuard low-level config
  directly instead of delegating to a profile/config service.
- Shipping debug logs that expose certificates, usernames, endpoints, keys, or
  tunnel traffic metadata.

## References

- [networkextension.md](references/networkextension.md) - Host app profile install, preferences lifecycle, status, on-demand, kill switch.
- [tunnelkit.md](references/tunnelkit.md) - TunnelKit modules, `NetworkExtensionVPN`, OpenVPN/WireGuard provider configuration.
- [packet-tunnel-provider.md](references/packet-tunnel-provider.md) - Extension lifecycle, network settings, packet flow, teardown.
- [entitlements-release.md](references/entitlements-release.md) - Capabilities, bundle IDs, App Groups, Keychain Sharing, archive checks.
- [debugging.md](references/debugging.md) - Install/connect failures, status triage, extension logs, data counters.
