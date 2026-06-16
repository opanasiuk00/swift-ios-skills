A team is building an iOS 26 SwiftUI paywall for monthly and yearly subscriptions. Their draft custom Buy button calls `product.purchase(options:)`, unlocks premium when any current entitlement exists for the product, starts `Transaction.updates` only after the paywall appears, and finishes each purchase before delivery. They also forgot restore purchases and policy links.

Write a concise StoreKit implementation review that corrects the purchase path, transaction listener timing, entitlement checks, pending purchase handling, restore path, verification, and transaction finishing order.
