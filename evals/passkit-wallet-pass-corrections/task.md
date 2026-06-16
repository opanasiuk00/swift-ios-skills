# Wallet Pass Plan Review

## Problem

A teammate proposes this Wallet pass flow:

- Load a `.pkpass`.
- Show a normal SwiftUI `Button` labeled "Add to Wallet".
- Use `PKPassLibrary.isPassLibraryAvailable()` to decide whether the device can
  add the pass.
- List every Wallet pass with `passes()`.
- Update the pass later by generating a new serial number.

Review the plan and replace it with correct PassKit guidance for presenting,
checking capability, reading accessible passes, and updating an existing pass.

## Output

Create a Markdown file named `passkit-wallet-pass-corrections.md`.
