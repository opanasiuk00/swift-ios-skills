# VPN Debugging

Use this reference for install, connect, extension, and traffic failures.

## Contents

- [Triage Order](#triage-order)
- [Install Failures](#install-failures)
- [Connect Failures](#connect-failures)
- [Extension Logging](#extension-logging)
- [TunnelKit Signals](#tunnelkit-signals)

## Triage Order

1. Confirm device testing. Many entitlement, prompt, and VPN lifecycle issues
   are not meaningful on simulator.
2. Check signed entitlements for the app and extension.
3. Remove stale VPN profiles after bundle ID or entitlement changes.
4. Reinstall the profile, save preferences, reload preferences, then start.
5. Watch `NEVPNStatusDidChange`.
6. Check extension logs and shared App Group last-error fields.
7. Validate server config and credentials outside the app when possible.

## Install Failures

Common causes:

- Packet Tunnel entitlement missing from app or extension App ID.
- `providerBundleIdentifier` does not match the extension bundle ID.
- Profile update started from stale manager without preferences reload.
- Old profile still installed for a previous extension bundle ID.
- `providerConfiguration` contains a non-property-list value.
- The user denied or removed VPN profile permission.

Fix by removing existing managers, reinstalling with a fresh manager, saving,
reloading, and starting only after reload.

## Connect Failures

Separate accepted start requests from real tunnel readiness:

- `startVPNTunnel()` can succeed while the extension later fails.
- `.connecting` stuck usually means provider setup, server reachability,
  authentication, or network settings did not finish.
- `.invalid` points to profile/capability/configuration problems.
- Fast `.connecting` to `.disconnected` often means provider crash or thrown
  start error.

Check the extension process logs first, then shared last-error fields.

## Extension Logging

Log from the extension with privacy masking:

- lifecycle: start options, stop reason, reasserting
- config profile ID, not raw secrets
- server endpoint, unless product policy treats it as private
- network settings summary
- authentication result category, not password/token data
- packet/session counters
- provider errors

Use App Group files for debug logs that the host app can export. Mask private
data by default and require an explicit user/debug build path to unmask.

## TunnelKit Signals

TunnelKit provider configurations commonly expose shared diagnostics through
App Group defaults:

- OpenVPN data count
- last connection date
- server-pushed configuration
- last error
- debug log URL
- WireGuard last error

Use these to show support diagnostics, but keep UI state driven by
`NEVPNStatusDidChange` and provider errors rather than polling only shared
defaults.
