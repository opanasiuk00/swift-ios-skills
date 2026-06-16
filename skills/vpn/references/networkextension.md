# NetworkExtension VPN Host App

Use this reference when implementing or reviewing the host app side of a custom
VPN profile. The host app owns profile installation, system permission prompts,
connect/disconnect commands, and user-facing state.

Official Apple docs:

- `NETunnelProviderManager`: https://sosumi.ai/documentation/networkextension/netunnelprovidermanager
- `NETunnelProviderProtocol`: https://sosumi.ai/documentation/networkextension/netunnelproviderprotocol
- `NEVPNManager`: https://sosumi.ai/documentation/networkextension/nevpnmanager
- `NEVPNStatus`: https://sosumi.ai/documentation/networkextension/nevpnstatus

## Contents

- [Manager Lifecycle](#manager-lifecycle)
- [Profile Installation](#profile-installation)
- [Status Handling](#status-handling)
- [On-Demand and Kill Switch](#on-demand-and-kill-switch)
- [Credential Boundary](#credential-boundary)

## Manager Lifecycle

Use `NETunnelProviderManager` for custom packet tunnel VPN protocols. The
manager object configures a VPN profile stored in Network Extension
preferences. Treat preferences as the source of truth:

1. Load existing managers with `NETunnelProviderManager.loadAllFromPreferences()`.
2. Reuse the manager matching the extension bundle ID when updating a profile.
3. Configure `localizedDescription`, `protocolConfiguration`, `onDemandRules`,
   `isOnDemandEnabled`, and `isEnabled`.
4. Call `saveToPreferences()`.
5. Call `loadFromPreferences()` again.
6. Start with `manager.connection.startVPNTunnel()`.

The reload step matters because the object returned after save is not always
the object the system will use for the approved profile.

## Profile Installation

Create a `NETunnelProviderProtocol` for the packet tunnel extension:

```swift
func makeProtocol(profile: VPNProfile, passwordRef: Data?) -> NETunnelProviderProtocol {
    let proto = NETunnelProviderProtocol()
    proto.providerBundleIdentifier = "com.example.app.PacketTunnel"
    proto.serverAddress = profile.serverAddress
    proto.username = profile.username
    proto.passwordReference = passwordRef
    proto.disconnectOnSleep = false
    proto.includeAllNetworks = profile.killSwitchEnabled
    proto.providerConfiguration = [
        "profileID": profile.id,
        "protocol": profile.protocolKind.rawValue
    ]
    return proto
}
```

Keep `providerConfiguration` small and serializable. Use IDs, feature flags,
transport names, server metadata, and encoded non-secret protocol config. Do
not use it as a secret store.

## Status Handling

Observe `.NEVPNStatusDidChange` and map `NEVPNStatus` into app state:

- `.connected`: tunnel is active.
- `.connecting` and `.reasserting`: show connecting/reconnecting.
- `.disconnecting`: show disconnecting.
- `.disconnected`: stopped or failed after cleanup.
- `.invalid`: profile is missing, disabled, corrupted, or no longer matches
  app/extension entitlements.

Do not assume `startVPNTunnel()` returning without throwing means connected.
It means the start request was accepted. The extension can still fail during
configuration, authentication, routing, or packet setup.

## On-Demand and Kill Switch

Use on-demand rules only when the product needs automatic reconnect or
per-interface behavior. Store the intent in the user profile and make generated
rules explicit in code review.

`NETunnelProviderProtocol.includeAllNetworks` is commonly used for kill-switch
behavior. Test it on a physical device with:

- Wi-Fi to cellular transitions.
- Captive portals.
- Local network access.
- DNS failure.
- Server unreachable.
- Sleep/wake and app relaunch.

## Credential Boundary

Store passwords, private keys, tokens, and identities in Keychain. Use:

- `passwordReference` for password-like credentials.
- Keychain access groups when the extension must read the same item.
- App Group only for non-secret shared state such as last error, data counters,
  log paths, and profile IDs.

If a provider needs a full config blob containing secrets, split the config:
put non-secret routing/protocol data in `providerConfiguration` and secrets in
Keychain keyed by a profile ID.
