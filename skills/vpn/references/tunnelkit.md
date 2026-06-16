# TunnelKit Integration

Use this reference when a VPN app uses TunnelKit or a fork with OpenVPN and
WireGuard modules. The local example studied for this skill is
`/Users/kostyaopanasiuk/Documents/GitHub/HideMyName/tunnelkit_hmn`.

## Contents

- [Module Split](#module-split)
- [Host App Wrapper](#host-app-wrapper)
- [OpenVPN Provider Configuration](#openvpn-provider-configuration)
- [WireGuard Provider Configuration](#wireguard-provider-configuration)
- [Build and Licensing Notes](#build-and-licensing-notes)

## Module Split

TunnelKit separates concerns:

- `TunnelKitManager`: host-app VPN abstraction over NetworkExtension.
- `TunnelKitOpenVPNManager`: OpenVPN provider configuration for the host app.
- `TunnelKitOpenVPNAppExtension`: `OpenVPNTunnelProvider` for the extension.
- `TunnelKitWireGuardManager`: WireGuard provider configuration for the host app.
- `TunnelKitWireGuardAppExtension`: `WireGuardTunnelProvider` for the extension.
- Core/protocol modules: crypto, packets, configuration parsing, OpenVPN or
  WireGuard protocol internals.

Keep app code at the manager/configuration layer unless you are fixing protocol
internals.

## Host App Wrapper

`NetworkExtensionVPN` wraps the usual manager lifecycle:

- `prepare()` warms NetworkExtension preferences.
- `install(_:configuration:extra:)` builds and saves a profile.
- `reconnect(after:)` stops if needed, waits, then starts.
- `disconnect()` stops all matching managers and disables on-demand.
- `uninstall()` removes profiles from preferences.

This wrapper still follows the same invariant as raw NetworkExtension:
save preferences, reload preferences, then start from the reloaded manager.

Use the wrapper from a service or manager, not directly from a view controller:

```swift
final actor VPNService {
    private let vpn = NetworkExtensionVPN()
    private let tunnelBundleID: String

    init(tunnelBundleID: String) {
        self.tunnelBundleID = tunnelBundleID
    }

    func connect(configuration: some NetworkExtensionConfiguration,
                 extra: NetworkExtensionExtra?) async throws {
        await vpn.prepare()
        try await vpn.install(tunnelBundleID, configuration: configuration, extra: extra)
        try await vpn.reconnect(after: .milliseconds(300))
    }

    func disconnect() async {
        await vpn.disconnect()
    }
}
```

## OpenVPN Provider Configuration

Build OpenVPN configuration in a profile/config service:

```swift
var builder = OpenVPN.ConfigurationBuilder()
builder.ca = ca
builder.cipher = .aes256cbc
builder.digest = .sha512
builder.compressionFraming = .compLZO
builder.renegotiatesAfter = nil
builder.remotes = [Endpoint(hostname, EndpointProtocol(.udp, port))]
builder.tlsWrap = TLSWrap(strategy: .auth, key: tlsKey)
builder.mtu = 1350
builder.routingPolicies = [.IPv4, .IPv6]

let cfg = builder.build()
var providerConfiguration = OpenVPN.ProviderConfiguration(
    title,
    appGroup: appGroup,
    configuration: cfg
)
providerConfiguration.shouldDebug = false
providerConfiguration.masksPrivateData = true
```

Review server compatibility carefully:

- Cipher and digest must match the server policy.
- Compression framing must match the server profile; wrong framing can cause
  immediate tunnel shutdown.
- TLS auth/crypt keys and directions must match the `.ovpn` profile.
- Unsupported `.ovpn` features need fallback or rejection before install.
- Multiple remotes, route literals, proxy settings, fragmentation, and external
  file references may not be supported by a TunnelKit fork.

## WireGuard Provider Configuration

Build WireGuard configuration from validated keys and endpoint values:

```swift
var builder = try WireGuard.ConfigurationBuilder(clientPrivateKey)
builder.addresses = [clientAddress]
builder.dnsServers = ["1.1.1.1", "1.0.0.1"]
try builder.addPeer(serverPublicKey, endpoint: "\(serverAddress):\(serverPort)")
builder.addDefaultGatewayIPv4(toPeer: 0)

let providerConfiguration = WireGuard.ProviderConfiguration(
    title,
    appGroup: appGroup,
    configuration: builder.build()
)
```

Validate:

- Private/public/pre-shared keys are valid base64 WireGuard keys.
- `AllowedIPs` express split tunnel vs default route intentionally.
- DNS servers and MTU match product policy.
- Endpoint host/port are reachable and preserved across reconnects.
- Private keys are stored in Keychain or a protected profile store, not logs.

## Build and Licensing Notes

WireGuard bridge builds can require an external build target for the Go bridge.
OpenVPN builds may involve OpenSSL/LZO/C code. Keep these checks in release
reviews:

- The tunnel extension links only frameworks allowed inside `.appex`.
- Any generated `Frameworks` folder inside the extension bundle is removed
  before App Store archive validation when the build setup creates it.
- Bitcode guidance in older TunnelKit docs is historical; current Xcode no
  longer uses iOS bitcode for App Store submissions.
- Review TunnelKit/fork licensing before shipping proprietary apps.
