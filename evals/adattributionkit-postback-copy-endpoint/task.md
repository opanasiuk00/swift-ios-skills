# Advertised App Postback Copy Setup

## Problem/Feature Description

An advertised app team is adding server-side ingestion for attribution reports. They want the app to receive copies of winning reports, including when an existing user returns through an ad. Their backend team owns a few HTTPS hosts and needs to know what route to implement, while the app team needs a concise launch and conversion-window checklist.

The output should be practical enough for an app engineer and backend engineer to split the work without confusing app configuration, server routing, postback timing, and JSON payload values.

## Output Specification

Create a file named `adattributionkit-postback-copy-setup.md` containing:

- an advertised-app Info.plist snippet;
- server endpoint routing requirements;
- first-launch/conversion update guidance;
- a compact postback timing summary;
- re-engagement handling notes; and
- a short note about postback JSON values the server should parse.
