Review this HealthKit setup plan for an iOS 26/iPadOS app:

- The team says HealthKit never works on iPad.
- The app creates `HKHealthStore` before any HealthKit availability check.
- The plan treats `authorizationStatus(for:)` as proof that read permission was denied.
- The team assumes denied reads always return empty arrays.

Give concise corrected guidance with Swift where useful.
