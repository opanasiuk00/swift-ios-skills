# Packet Tunnel Provider

Use this reference for `NEPacketTunnelProvider` subclasses and TunnelKit app
extension providers.

Official Apple docs:

- `NEPacketTunnelProvider`: https://sosumi.ai/documentation/networkextension/nepackettunnelprovider
- `startTunnel(options:completionHandler:)`: https://sosumi.ai/documentation/networkextension/nepackettunnelprovider/starttunnel%28options:completionhandler:%29
- `NEPacketTunnelNetworkSettings`: https://sosumi.ai/documentation/networkextension/nepackettunnelnetworksettings

## Contents

- [Lifecycle](#lifecycle)
- [Network Settings](#network-settings)
- [Packet Flow](#packet-flow)
- [Shared State](#shared-state)

## Lifecycle

For raw NetworkExtension providers:

```swift
final class PacketTunnelProvider: NEPacketTunnelProvider {
    override func startTunnel(
        options: [String: NSObject]?,
        completionHandler: @escaping (Error?) -> Void
    ) {
        do {
            let config = try loadProviderConfiguration()
            let settings = try makeNetworkSettings(config)
            setTunnelNetworkSettings(settings) { error in
                if let error {
                    completionHandler(error)
                    return
                }
                self.startPacketLoop(config)
                completionHandler(nil)
            }
        } catch {
            completionHandler(error)
        }
    }

    override func stopTunnel(
        with reason: NEProviderStopReason,
        completionHandler: @escaping () -> Void
    ) {
        stopPacketLoop()
        completionHandler()
    }
}
```

For TunnelKit providers, subclass the library provider:

```swift
import TunnelKitOpenVPNAppExtension

final class PacketTunnelProvider: OpenVPNTunnelProvider {
    override func startTunnel(options: [String: NSObject]? = nil) async throws {
        dataCountInterval = 3
        try await super.startTunnel(options: options)
    }
}
```

or:

```swift
import TunnelKitWireGuardAppExtension

final class PacketTunnelProvider: WireGuardTunnelProvider {
}
```

## Network Settings

Call `setTunnelNetworkSettings` before reporting a successful start. Settings
usually include:

- `tunnelRemoteAddress`
- IPv4 and/or IPv6 addresses
- included/excluded routes
- DNS servers and match domains
- MTU when required by protocol/server
- proxy settings only when deliberately supported

For OpenVPN, build settings from local config plus server-pushed options. For
WireGuard, build settings from interface address, peer allowed IPs, DNS, MTU,
and endpoint route policy.

## Packet Flow

The extension owns packet I/O through `packetFlow`. The host app should never
read or write packet data. In raw providers:

- Read packets from `packetFlow.readPackets`.
- Encrypt/encapsulate them to the tunnel transport.
- Decode inbound transport packets.
- Write packets back with `packetFlow.writePackets`.

In TunnelKit, this is handled by the provider implementation and protocol
modules. Avoid modifying packet code unless fixing protocol behavior.

## Shared State

Use App Group `UserDefaults` or files for non-secret diagnostics:

- last connection date
- last tunnel error
- data counters
- debug log path
- server-pushed configuration snapshot

Mask private data in logs by default. Do not store private keys, passwords,
tokens, full client cert material, or traffic payloads in shared defaults.
