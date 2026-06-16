# Audio Accessory Automatic Switching Flow

## Problem/Feature Description

A headphones team already uses AccessorySetupKit to pair its accessory and
receive an `ASAccessory`. The next ticket is to add AudioAccessoryKit support
for automatic audio switching and to update the system when the firmware
reports that the headphones moved between on-head and off-head states.

Write a concise implementation note for the iOS engineers. The note should be
specific enough that a developer can see the correct framework roles and the
shape of the Swift calls, but it does not need to be a complete app.

## Output Specification

Create a file named `audioaccessorykit-switching-flow.md` containing:

- the setup sequence from paired accessory to audio-switching registration;
- a minimal Swift example for registering the accessory;
- a minimal Swift example for updating wear placement;
- error-handling guidance; and
- a short list of role or lifecycle constraints that would prevent common
  integration mistakes.
