# CarPlay Messaging Review

## Problem/Feature Description

A communication app team is updating its CarPlay message list for iOS 26. Their proposed row model was copied from an older prototype:

```swift
let message = CPMessageListItem(
    conversationIdentifier: conversation.id,
    text: conversation.title,
    leadingConfiguration: CPMessageListItem.LeadingConfiguration(
        leadingItem: .init(text: conversation.initials, textStyle: .abbreviated),
        unread: conversation.isUnread),
    trailingConfiguration: CPMessageListItem.TrailingConfiguration(
        trailingItem: .init(text: conversation.time, textStyle: .abbreviated)),
    trailingText: nil,
    trailingImage: conversation.badge)

message.handler = { item, completion in
    openConversationDetail(for: conversation.id)
    completion()
}
```

Review the proposal and explain what should change before the team ships the CarPlay communication experience.

## Output Specification

Create a file named `carplay-communication-review.md` containing:

- A short diagnosis of the API and behavior problems.
- Corrected Swift that uses current CarPlay communication list APIs.
- Guidance on what row selection should do in CarPlay.
- A recommendation for what to use if the product really needs app-owned drill-in content.
