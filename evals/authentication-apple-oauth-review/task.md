# Sign in with Apple and OAuth Review

## Problem/Feature Description

An app team drafted a login plan with Sign in with Apple for new accounts, saved password suggestions for returning users, GitHub OAuth, cached profile data, local Face ID re-authentication before account deletion, and refresh-token storage. They want a focused review before implementation, not a general security whitepaper.

## Output Specification

Write the must-have AuthenticationServices, LocalAuthentication, and token-handling checks the iOS implementation should satisfy. Cover the Sign in with Apple setup and credential lifecycle, existing account flows, third-party OAuth session presentation, biometric re-authentication boundaries, and secure token storage.
