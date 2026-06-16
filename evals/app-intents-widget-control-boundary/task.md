A smart-home app is planning three surfaces:

- A configurable Home Screen widget showing a selected room and favorite accessory.
- A Control Center toggle for an accessory's power state.
- A Siri response that shows live accessory status in a custom snippet after a user asks to check a room.

The draft uses one `WidgetConfigurationIntent` with a `perform()` method for all three surfaces, gives the control's accessory parameter a non-optional value with no default, mutates accessory state from the snippet intent, and includes a full WidgetKit timeline provider rewrite in the App Intents plan.

Write a concise review and corrected architecture. Focus on which App Intents protocols belong to each surface, where side effects should live, and what should stay in WidgetKit or another layer.
