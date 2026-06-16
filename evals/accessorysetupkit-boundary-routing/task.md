# Smart Home Onboarding Skill Boundary

## Problem/Feature Description

A product proposal asks for a single implementation guide covering smart-home lights. The app needs to add Matter lights to a user's home, assign them to rooms, read and write accessory characteristics, and create automations. The proposal also mentions nearby discovery and says some accessories may advertise over Bluetooth during setup.

Write a routing note for the engineering team explaining which Apple framework domain should own this implementation guidance and what should be out of scope for a lower-level accessory discovery guide.

## Output Specification

Create a file named `skill-boundary-note.md` containing:

- A recommended owning skill/framework domain for the smart-home implementation.
- A concise explanation of why that domain owns homes, rooms, characteristics, automations, and Matter onboarding.
- A concise explanation of what a Bluetooth/Wi-Fi accessory discovery guide can cover without taking over the smart-home implementation.
- A short list of examples that should be routed away from the lower-level accessory discovery guide.

Do not write implementation code for the smart-home app.
