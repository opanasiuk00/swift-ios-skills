You are reviewing an App Clip implementation plan for a coffee shop app.

The full app bundle identifier is `com.example.cafe`; the proposed App Clip bundle identifier is `com.example.cafe.Clip`. The team wants:

- A default App Clip experience for their website.
- Advanced experiences for individual store locations reached from QR codes, NFC tags, and App Clip Codes.
- A SwiftUI App Clip UI.
- Some UIKit scene delegate code that still handles universal-link routing in shared modules.
- The full app to take over every invocation after the user installs it.

Write a concise engineering review that identifies the target setup, entitlement and associated-domain requirements, experience configuration, and invocation routing changes the team should make before implementation.