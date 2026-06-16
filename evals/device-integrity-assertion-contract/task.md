# App Attest Assertion Contract

## Problem/Feature Description

A subscription app already enrolled App Attest keys and now wants to protect premium-content download requests. The team needs a client/server contract for what the app signs and what the backend verifies before serving protected content.

## Output Specification

Write an implementation-oriented assertion design. Cover the client data shape, how it binds to the request, how replay is prevented, how the server verifies the assertion, and what App Attest does and does not replace.
