---
name: ios-architecture
description: "Select, review, scaffold, or migrate iOS app architecture patterns for Swift 6.3, SwiftUI, and UIKit apps. Use when choosing between UIKit MVC, MV with @Observable, MVVM, MVI, TCA (The Composable Architecture), Clean Architecture, Coordinator/Router, Repository, dependency injection, or SPM feature modularization; when evaluating project structure, module boundaries, dependency direction, feature ownership, test seams, or migration strategy; or when reviewing whether an iOS app's current architecture is appropriate."
---

# iOS Architecture

Select the simplest architecture that keeps feature behavior understandable,
testable, and changeable. Prefer current SwiftUI and Swift concurrency patterns,
but keep UIKit and hybrid apps in scope.

## Contents

- [Scope Boundary](#scope-boundary)
- [Use Workflow](#use-workflow)
- [Architecture Selection](#architecture-selection)
- [Core Rules](#core-rules)
- [Reference Routing](#reference-routing)
- [Structure Templates](#structure-templates)
- [Quick Decisions](#quick-decisions)
- [Common Mistakes](#common-mistakes)
- [Review Checklist](#review-checklist)
- [References](#references)

## Scope Boundary

This skill owns app structure decisions: pattern selection, module boundaries,
dependency direction, dependency injection shape, repository/use-case seams,
navigation ownership, migration path, and structural test strategy.

Route detailed SwiftUI state mechanics to sibling skills when needed:

- `swiftui-patterns`: `@State`, `@Bindable`, `@Environment`, local edit state,
  view composition, and `@Observable` mechanics inside SwiftUI views.
- `swiftui-navigation`: `NavigationStack`, `NavigationSplitView`,
  route models, sheets, tabs, deep links, and URL routing implementation.
- `swift-concurrency`: `@MainActor`, `Sendable`, task cancellation, actors,
  strict-concurrency diagnostics, and data-race fixes.
- `swift-testing`: `@Test`, `#expect`, fixtures, mocks, stubs, parameterized
  tests, and suite organization.

## Use Workflow

1. Identify app size, team size, platform floor, UIKit/SwiftUI mix, data sources,
   offline needs, and how much state must be coordinated across screens.
2. Choose the smallest pattern that gives clear ownership and test seams.
3. Define dependency direction before naming folders or modules.
4. Read the relevant reference file before giving implementation-level code.
5. Push heavy examples into references; keep the answer focused on the user's
   current decision or migration.

## Architecture Selection

| Situation | Default choice | Escalate when |
|---|---|---|
| Simple SwiftUI feature or small app | MV with `@Observable` model/store | Business rules or presentation transforms grow hard to test |
| Simple UIKit feature or legacy UIKit app | UIKit MVC with custom `UIView` + injected services | Controllers accumulate business logic, networking, or cross-flow routing |
| Screen with meaningful presentation logic | MVVM with `@Observable` ViewModel | State spans many child features or effects need strict ordering |
| Complex state machine | MVI or TCA | The team needs exhaustive reducer/effect tests and accepts TCA conventions |
| Enterprise/domain-heavy app | Clean Architecture | Layer count is ceremonial and slows feature work |
| Many teams or slow builds | Local SPM feature modules | Boundaries are stable enough to justify package overhead |
| Complex UIKit/hybrid navigation | Coordinator/Router | SwiftUI route models can own the flow cleanly |
| Existing VIPER app | Maintain and simplify VIPER boundaries | New SwiftUI work can be isolated with lighter patterns |

Default recommendation for new SwiftUI work: start with MV or MVVM using
`@Observable`, async/await, protocol-backed dependencies, and value-type state.
Add Clean, TCA, or package modularity only when the codebase has the complexity
that pays for those seams.

## Core Rules

1. Keep dependency direction explicit. UI depends on feature/application logic;
   domain logic does not depend on UI frameworks.
2. Do not make every dependency a protocol by reflex. Add protocols at external
   boundaries, unstable seams, and test seams that actually need substitution.
3. Keep ViewModels and stores on the main actor when they mutate UI-observed
   state. Delegate long-running work to async services, repositories, actors, or
   clients.
4. Keep networking, persistence, Keychain, location, analytics, and SDK calls
   behind clients or repositories. Views should not talk to raw infrastructure.
5. Map DTOs, database models, and domain/view models deliberately. Do not leak
   transport or persistence shapes into UI state unless the app is tiny and the
   tradeoff is intentional.
6. Feature modules should not import each other. Share contracts through core
   modules, route through the app shell, or lift shared behavior into a common
   dependency.
7. Treat TCA, Clean Architecture, and SPM modularization as architectural costs,
   not automatic upgrades.
8. Prefer value types for state and models. Use reference types for identity,
   observation, shared services, actors, and lifecycle-managed objects.
9. Localize user-facing errors at the presentation boundary. Preserve typed
   errors or domain failures inside lower layers.
10. Review architecture by behavior and change cost, not by folder count.

## Reference Routing

Read only the references relevant to the user's prompt:

| User is asking about | Read |
|---|---|
| MVVM, ViewModels, `@Observable`, view-state mapping | `references/mvvm.md` |
| UIKit MVC, custom `UIView`, `UIViewController`, target/action, delegates, simple controller-owned state | `references/uikit-mvc.md` |
| Layers, use cases, entities, DTOs, repository protocols | `references/clean.md` |
| Reducers, stores, effects, `@ObservableState`, `TestStore` | `references/tca.md` |
| SPM packages, feature modules, build times, dependency graphs | `references/modular.md` |
| Repository, Coordinator/Router, DI, error flow, POP | `references/patterns.md` |

If the prompt spans multiple areas, load the narrowest set of references and
name the tradeoff between them.

## Structure Templates

### Small SwiftUI App

```text
MyApp/
+-- App/
+-- Features/
|   +-- Home/
|   |   +-- HomeView.swift
|   |   +-- HomeModel.swift or HomeViewModel.swift
|   +-- Settings/
+-- Models/
+-- Clients/
+-- Resources/
+-- Tests/
```

Use this when the app has few screens and simple data flow. Avoid Clean
Architecture folders until there is real domain behavior to isolate.

### UIKit MVC Feature

```text
FeatureName/
+-- Controller/
|   +-- FeatureController.swift
+-- View/
|   +-- FeatureView.swift
+-- Model/
|   +-- FeatureModel.swift
+-- Assembly/
    +-- FeatureAssembly.swift
```

Use this for UIKit screens where a `UIViewController` manages lifecycle,
target/action, delegates, view state, and navigation, while a custom `UIView`
owns layout and reusable managers/services own network, storage, or business
work. Escalate to MVVM or Clean only after controller responsibilities stop
being screen-level coordination.

### Layered Feature App

```text
MyApp/
+-- App/
|   +-- CompositionRoot.swift
|   +-- AppRouter.swift
+-- Domain/
|   +-- Entities/
|   +-- UseCases/
|   +-- Repositories/        # protocols/contracts
+-- Data/
|   +-- API/
|   +-- Persistence/
|   +-- Repositories/        # implementations
|   +-- Mappers/
+-- Presentation/
|   +-- Features/
+-- Tests/
```

Use this when business rules, offline behavior, or data mapping need clear
separation from the UI.

### Modular App

```text
MyApp.xcodeproj
+-- App/
+-- Packages/
    +-- CoreKit/
    +-- DesignSystem/
    +-- NetworkKit/
    +-- SharedServices/
    +-- Features/
        +-- HomeFeature/
        +-- ProfileFeature/
```

Use this when build times, team ownership, or dependency boundaries are already
hurting. Keep the app target as the composition root.

## Quick Decisions

- `@Observable` vs `ObservableObject`: use `@Observable` for iOS 17+ code; use
  `ObservableObject` only for older deployment targets or existing Combine-era
  code.
- MV vs MVVM: use MV for simple SwiftUI features; use MVVM when display logic,
  side effects, or tests need a separate object.
- UIKit MVC: keep it for simple UIKit screens and existing UIKit codebases; use
  injected managers/services plus custom `UIView` before adding a ViewModel.
- Clean Architecture: use when domain rules and data mapping justify layers; do
  not create empty use cases that just forward repository calls.
- TCA: use when explicit state/effect modeling and reducer tests are more
  valuable than the framework overhead.
- Repository: use for data-source boundaries and caching/offline policy; avoid
  repositories that only rename a single service method.
- Coordinator/Router: use for cross-feature navigation ownership; keep simple
  local navigation in SwiftUI route state.
- SPM modules: add after boundaries are stable or build/team pressure is real.

## Common Mistakes

1. Starting with Clean Architecture or TCA because the app might grow later.
2. Creating a ViewModel for every subview instead of every stateful screen or
   feature.
3. Putting networking, database, Keychain, or analytics calls directly in views
   or UIKit view controllers.
4. Letting feature modules import each other.
5. Making protocols for every concrete type without a substitution need.
6. Hiding dependencies in singletons instead of injecting them at composition
   boundaries.
7. Letting DTOs or persistence objects become the app's domain model by default.
8. Moving SwiftUI property-wrapper mechanics into architecture answers instead
   of routing them to `swiftui-patterns`.
9. Treating folder structure as proof of architecture quality.
10. Adding packages so early that navigation, previews, and tests become slower
    than the original problem.
11. Calling UIKit MVC "bad" by default. UIKit's MVC split is fine when the
    controller coordinates a screen and delegates real work to services,
    managers, models, and custom views.

## Review Checklist

- [ ] The chosen pattern matches current complexity, not imagined future scale.
- [ ] Dependency direction is explicit and acyclic.
- [ ] UI-observed state is main-actor safe.
- [ ] External systems are behind clients, repositories, or adapters.
- [ ] Domain entities are not polluted by transport, persistence, or UI concerns.
- [ ] Feature modules do not import sibling features.
- [ ] Navigation ownership is clear at local, feature, and app-shell levels.
- [ ] UIKit MVC controllers own screen coordination only; layout lives in views
      and external work lives in injected dependencies.
- [ ] Tests target the behavior-owning layer: model/store, ViewModel, reducer,
      use case, repository, or router.
- [ ] The answer names when not to use heavier architecture.
- [ ] Relevant reference files were loaded before detailed implementation code.

## References

- `references/mvvm.md` -- MVVM with `@Observable`, ViewModel patterns, testing.
- `references/uikit-mvc.md` -- UIKit MVC with custom views, controller
  responsibilities, managers/services, assemblies, delegates, and escalation
  rules.
- `references/clean.md` -- Clean Architecture layers, DI, use cases, mappers.
- `references/tca.md` -- The Composable Architecture state, reducers, effects,
  dependencies, and tests.
- `references/modular.md` -- SPM modules, feature modules, dependency rules,
  and build optimization.
- `references/patterns.md` -- Repository, Coordinator/Router, DI, error
  handling, protocol-oriented design, and code organization.
