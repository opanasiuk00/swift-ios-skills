You are designing a parking-meter App Clip.

The user can scan a meter, start a short parking session, and optionally install the full app afterward. The product requirements say:

- Preserve enough state for the full app to continue the pending parking session.
- Use Sign in with Apple if the user chooses to identify themselves.
- Send a short-lived reminder notification soon after launch.
- Reopen the right meter/session if the user taps that notification.
- Confirm that the user is physically near the meter without asking for continuous location access.

Write an implementation checklist for the App Clip and the full app. Focus on the App Clip-specific boundaries, plist keys, APIs, security caveats, and handoff behavior.