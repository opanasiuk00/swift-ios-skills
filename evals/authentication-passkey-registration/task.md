# Passkey Registration and Sign-In Plan

## Problem/Feature Description

The account team is adding passwordless sign-in to an iOS app for accounts on `example.com`. The backend can mint WebAuthn challenges and verify responses. Product wants platform passkeys as the primary flow, an option for users with physical security keys, and inline suggestions from the username field when a returning user starts sign-in.

## Output Specification

Write a concise implementation plan that an iOS engineer can use before opening Xcode. Include the app entitlement/domain setup, the AuthenticationServices request flow for registration and sign-in, where server verification happens, and the expected AutoFill and physical-security-key boundaries.
