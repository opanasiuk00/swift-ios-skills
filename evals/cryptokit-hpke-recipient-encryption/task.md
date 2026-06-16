# CryptoKit HPKE Recipient Encryption

## Problem/Feature Description

A team is replacing a custom ECDH + HKDF + AES-GCM message format in an iOS app. They need to encrypt payloads for a recipient public key using current CryptoKit APIs and want the Swift details that avoid common implementation mistakes.

Cover the recommended CryptoKit API, platform availability, ciphersuite choice, how ciphertext and key material are transmitted, how associated metadata is authenticated, and what ordering/state caveats matter for multiple messages.

## Output Specification

Create `cryptokit-hpke-recipient-encryption.md` with a concise implementation outline and Swift snippets where they clarify the flow.
