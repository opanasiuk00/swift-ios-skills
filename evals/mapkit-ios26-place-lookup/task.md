# Delivery Address Modernization

## Problem/Feature Description

A delivery app is modernizing its address and place lookup layer for the next iOS release while still supporting existing route planning. The app needs to turn typed delivery addresses into places, reverse map taps into readable addresses, format addresses for receipts, create a place reference from a coordinate when no provider place ID exists, and offer bicycle routing where the platform supports it.

Prepare a short implementation note for the team. Focus on the MapKit/CoreLocation APIs and the availability boundaries that matter for a production codebase.

## Output Specification

Create `place-lookup-note.md` with:

- Swift snippets or pseudocode for forward geocoding, reverse geocoding, address formatting, place reference creation, and bicycle routing.
- The imports and availability annotations the team should use.
- A short migration checklist of mistakes to avoid.
