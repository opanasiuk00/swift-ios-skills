# Face ID Account Detail Gate

## Problem/Feature Description

A banking app wants to reveal a sensitive account detail only after local user
verification. The current design calls LocalAuthentication, checks the returned
success value, and then reads the account detail from app preferences. The team
also omitted the Face ID usage string from the app metadata.

The security lead wants a correction plan that can be handed to the iOS team
before implementation starts.

## Output Specification

Create `biometric-plan.md` with:

- the main security flaw in the current design,
- the corrected storage and retrieval architecture,
- the important platform constraints and recovery cases,
- and a short implementation checklist.
 
## Input Files

The proposed flow is:

```swift
func showAccountNumber() {
    let context = LAContext()
    context.evaluatePolicy(
        .deviceOwnerAuthenticationWithBiometrics,
        localizedReason: "Show account number"
    ) { success, error in
        guard success else { return }
        let accountNumber = UserDefaults.standard.string(forKey: "accountNumber")
        render(accountNumber)
    }
}
```
