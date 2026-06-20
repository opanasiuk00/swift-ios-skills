# Multi-Screen Flow and Navigation Inference

Use this reference when the user provides several Figma screens, a group of frames, an auth/onboarding flow, or screenshots that imply transitions between screens.

## Contents

- [1. Build a Screen Inventory](#1-build-a-screen-inventory)
- [2. Detect Screen Roles](#2-detect-screen-roles)
- [3. Extract Actions and Destinations](#3-extract-actions-and-destinations)
- [4. Map to Project Navigation](#4-map-to-project-navigation)
- [5. Implement Flow State](#5-implement-flow-state)
- [6. Uncertainty Rules](#6-uncertainty-rules)
- [7. Checklist](#7-checklist)

## 1. Build a Screen Inventory

Before coding, list every supplied frame/screenshot:

| Screen | Figma node | Role | Primary action | Secondary actions | Destination | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Login | `12:34` | auth login | Login | Forgot password, Sign up | Home or OTP | Needs credential validation |
| OTP | `12:78` | auth verification | Verify | Back, Resend | Home | Follows login |

Use Figma frame names, visible titles, button copy, input labels, component names, and relative ordering on the canvas. If the Figma MCP exposes prototype links or interactions, treat those as higher priority than inference from text.

## 2. Detect Screen Roles

Classify screens by intent, not just visual appearance:

- Login: email/password, phone login, social sign-in, "Login", "Sign in"
- Signup: registration fields, "Create account", "Sign up"
- OTP/verification: code fields, "Verify", "Resend"
- Forgot/reset password: email entry, reset code, new password
- Onboarding: paging, "Next", "Skip", "Get started"
- Permission prompt: permission explanation, "Allow", "Continue"
- Home/root: tab entry, dashboard, main content after auth/onboarding
- Detail: selected item content, product/device/profile details
- Settings/form: rows, toggles, user preferences
- Empty/error/loading states: same route with state, not usually separate navigation destinations

If multiple screens share one route but represent states of the same feature, implement them as state variants in one view rather than separate routes.

## 3. Extract Actions and Destinations

For each tappable element:

1. Prefer Figma prototype interaction destination when available.
2. If absent, infer from copy and screen set:
   - `Login`, `Sign in`, `Continue` on login -> authenticated root, OTP, or next auth step if supplied.
   - `Create account`, `Sign up` -> signup screen if supplied.
   - `Forgot password` -> reset password screen if supplied.
   - `Verify`, `Submit code` -> authenticated root or success screen.
   - `Next` -> next onboarding screen by canvas/order/name.
   - `Skip`, `Get started` -> final onboarding destination/root.
   - `Back`, close icon -> pop/dismiss using existing project behavior.
3. Inspect existing project route names and call sites before inventing route enum cases.
4. If destination is ambiguous, implement the visual screen and expose an action closure/router hook instead of hard-coding the wrong route.

Do not wire destructive actions, purchases, account creation, or real authentication side effects unless the project already has the required service/action pattern.

## 4. Map to Project Navigation

Use the target project's existing navigation pattern first:

- Existing router object -> add or reuse route cases and call router methods.
- `NavigationStack(path:)` -> push `Hashable` route/model values and add `.navigationDestination`.
- Tab app -> switch selected tab or route within that tab's independent stack.
- Modal screen -> use existing sheet/fullScreenCover routing style.
- Coordinator/TCA/feature reducer -> follow that architecture instead of local `@State` navigation.

Apply the `swiftui-navigation` skill before finalizing push/sheet/tab/router code. Apply `swiftui-patterns` for state ownership and `swiftui-layout-components` for layout choices.

## 5. Implement Flow State

Keep visual screens decoupled from navigation side effects where the project expects reusable views:

```swift
struct LoginView: View {
    let onLogin: () -> Void
    let onForgotPassword: () -> Void
    let onSignup: () -> Void

    var body: some View {
        VStack {
            Button("Login", action: onLogin)
            Button("Forgot password", action: onForgotPassword)
            Button("Sign up", action: onSignup)
        }
    }
}
```

Container/root views should own routes, selected tab, sheet destination, or environment router calls. Leaf views should usually expose closures unless the project already injects a router into leaf views.

For authentication forms, preserve project validation, networking, loading, disabled, error, and accessibility patterns. Do not create fake success transitions that bypass existing auth services unless the user explicitly requests a static prototype.

## 6. Uncertainty Rules

When uncertain, prefer explicit seams over wrong navigation:

- Name the inferred edge in the adaptation audit or implementation note.
- Use action closures for ambiguous destinations.
- Leave an explicit implementation note only if the project already accepts unfinished wiring notes and the user expects partial wiring.
- Ask the user only when the ambiguity changes data flow or could create harmful behavior.

Never silently connect a button to a screen just because it is nearby on the Figma canvas when prototype links, labels, or project route names point elsewhere.

## 7. Checklist

- Every supplied screen/frame has a role and node/screenshot reference.
- Primary and secondary actions are listed.
- Prototype links were used when available.
- Inferred edges are marked as inferred.
- Existing project route/router/tab/sheet patterns were inspected before adding navigation.
- Screens that are states of one route were implemented as state variants, not duplicate routes.
- Leaf views expose closures when navigation ownership belongs to the container/router.
- `swiftui-navigation`, `swiftui-patterns`, and `swiftui-layout-components` were applied before finalizing.
