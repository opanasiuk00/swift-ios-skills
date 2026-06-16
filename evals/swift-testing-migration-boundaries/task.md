# Swift Testing Migration Review

## Problem/Feature Description

A team is migrating XCTest unit tests to Swift Testing. Their plan is to keep the `XCTestCase` subclass, convert `setUp` and `tearDown` into a shared singleton fixture, put `@available` on the whole suite type for iOS 18 APIs, replace every XCTest assertion with `#expect` including `XCTUnwrap`, keep `XCTFail("missing user")` for guard-failure paths, and move UI tests into Swift Testing because they think it replaces XCTest everywhere. They also want to know whether XCTest and Swift Testing can coexist during the migration.

## Output Specification

Create `swift-testing-migration-review.md` with corrected migration guidance, concise Swift examples where useful, and a short review checklist. Do not create an Xcode project.
