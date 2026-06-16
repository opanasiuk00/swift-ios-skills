# Token Storage Review

## Problem/Feature Description

The mobile team is preparing a release that changes how OAuth tokens are cached
on device. They want a short security review before the helper is merged because
the app must support account logout, token rotation, and occasional background
refresh.

The helper currently writes the refresh token to preferences, stores access
tokens with a Keychain add call that ignores the result, leaves the protection
class implicit, and deletes any existing item before each save so duplicates do
not block the write.

## Output Specification

Create `security-review.md` with:

- a concise findings table with severity,
- the corrected storage/update strategy,
- the important error cases the implementation must handle,
- and a brief test checklist for the new helper.

## Input Files

The relevant helper shape is:

```swift
final class TokenStore {
    func save(refreshToken: String, accessToken: String) {
        UserDefaults.standard.set(refreshToken, forKey: "refresh")

        let deleteQuery: [String: Any] = [
            kSecClass as String: kSecClassGenericPassword,
            kSecAttrService as String: "com.example.auth",
            kSecAttrAccount as String: "access"
        ]
        SecItemDelete(deleteQuery as CFDictionary)

        let addQuery: [String: Any] = [
            kSecClass as String: kSecClassGenericPassword,
            kSecAttrService as String: "com.example.auth",
            kSecAttrAccount as String: "access",
            kSecValueData as String: Data(accessToken.utf8)
        ]
        SecItemAdd(addQuery as CFDictionary, nil)
    }
}
```
