# Bluetooth Headphones Framework Boundary

## Problem/Feature Description

A companion-app plan for Bluetooth headphones asks for one framework to cover
the setup picker, accessory permission flow, BLE service discovery, firmware
communication, and automatic audio switching. The team is considering using
AudioAccessoryKit for the whole flow.

Write a routing note that assigns each part of the work to the appropriate
Apple framework domain and explains what AudioAccessoryKit should and should
not own.

## Output Specification

Create a file named `audioaccessorykit-boundary-note.md` containing:

- a direct answer to whether AudioAccessoryKit should own the whole flow;
- the framework/domain that should own discovery, picker UI, and authorization;
- the framework/domain that should own BLE firmware communication;
- the framework/domain that should own post-pairing audio-switching support;
- the required sequencing between setup and audio registration; and
- examples of work that should be routed away from AudioAccessoryKit.
