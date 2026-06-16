# CarPlay Navigation Readiness

## Problem/Feature Description

A navigation team has an existing iPhone app with a mature map renderer and route engine. They want to add a CarPlay experience for route preview and turn-by-turn guidance, but the draft currently treats the car display like another UIKit screen.

Review the planned integration and write a practical implementation guide for iOS 26 that an app engineer can use before opening the Xcode project.

## Output Specification

Create a file named `carplay-navigation-readiness.md` containing:

- The Apple account, provisioning, entitlement, and project configuration needed for a navigation CarPlay app.
- The scene configuration and delegate shape the CarPlay entry point should use.
- Swift snippets for connecting the scene, setting up the root map experience, and starting guidance.
- The boundary between the app's map renderer and CarPlay-provided controls.
- A concise simulator and real-world test plan.
