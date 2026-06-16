# Matter Light Ecosystem Setup

## Problem/Feature Description

A smart-home ecosystem app wants to let people add Matter lights into the app's
own ecosystem from iOS. The engineering team needs implementation guidance for
the app request, setup discovery configuration, the MatterSupport extension
callbacks, optional setup-code handling, and post-setup app refresh.

## Output Specification

Create a file named `matter-light-ecosystem-setup.md` containing:

- The app and extension configuration checklist.
- Swift-oriented `MatterAddDeviceRequest` guidance.
- Optional setup-code handling when the app supplies the code.
- A MatterSupport extension handler outline with the important callbacks.
- A short note about what to refresh after `perform()` succeeds.

Do not present this as ordinary `HMHome.addAndSetupAccessories` setup or as an
AccessorySetupKit picker flow.
