# Smart-Home Framework Boundary

## Problem/Feature Description

A proposal asks for one Apple accessory guide to cover Matter light onboarding,
HomeKit rooms and automations, setup-only BLE discovery, GATT control after
selection, and joining a temporary Wi-Fi setup network.

Write a routing note that assigns each part to the right framework domain and
explains what belongs in the HomeKit skill.

## Output Specification

Create a file named `homekit-framework-boundary.md` containing:

- The recommended owner for Matter onboarding.
- The HomeKit-owned smart-home model and automation topics.
- The framework domain for setup-only Bluetooth or Wi-Fi discovery.
- The framework domain for post-selection BLE/GATT communication.
- The framework domain for temporary Wi-Fi setup-network joins.

Do not provide implementation code, lifecycle recipes, setup procedures, or
ordered method-call sequences. You may name representative framework types or
APIs only as routing labels.
