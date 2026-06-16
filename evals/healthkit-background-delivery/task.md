Review this background step-count sync plan:

- `enableBackgroundDelivery(for:frequency:)` is called with `.immediate` after the first dashboard screen appears.
- The `HKObserverQuery` is created only while that dashboard screen is visible.
- The observer query completion handler is skipped on error paths.
- QA plans to validate the behavior only in Simulator.

Explain what should change and why.
