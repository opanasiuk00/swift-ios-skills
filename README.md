# Swift iOS Skills

Agent skills for iOS, iPadOS, macOS, Swift, SwiftUI, and modern Apple framework development.

Every skill is self-contained. No skill depends on another. Install only what you need.

Release notes: [CHANGELOG.md](CHANGELOG.md).

## Contents

- [Install](#install)
  - [Recommended: any agent via skills CLI](#recommended-any-agent-via-skills-cli)
  - [Claude Code](#claude-code-via-plugin-marketplace)
  - [OpenAI Codex](#openai-codex)
  - [Claude Web App / Claude Desktop](#claude-web-app--claude-desktop)
  - [ChatGPT](#chatgpt)
- [Quick Start Tutorial](#quick-start-tutorial)
- [Plugin Bundles](#plugin-bundles-claude-code)
- [Skills](#skills)
  - [SwiftUI](#swiftui)
  - [Core Swift](#core-swift)
  - [App Experience Frameworks](#app-experience-frameworks)
  - [Data & Service Frameworks](#data--service-frameworks)
  - [AI & Machine Learning](#ai--machine-learning)
  - [iOS Engineering](#ios-engineering)
  - [Hardware & Device Integration](#hardware--device-integration)
  - [Platform Integration](#platform-integration)
  - [Gaming](#gaming)
- [Structure](#structure)

## Install

### Recommended: any agent via [skills CLI](https://github.com/vercel-labs/skills)

The skills CLI is the recommended install method.

Interactive install (recommended):

```sh
npx skills add opanasiuk00/swift-ios-skills
```

Running the default command opens the skills CLI UI so you can choose which skills to install and which agent(s) to install them for.

Install everything for any coding agent:

```sh
npx skills add opanasiuk00/swift-ios-skills --all
```

Use `--all` when you want the full set of 86 skills installed automatically for any coding agent.

Install specific skills directly:

```sh
npx skills add opanasiuk00/swift-ios-skills --skill <skill-name> --skill <skill-name>
```

Check for updates to installed skills:

```sh
npx skills check
```

Update installed skills:

```sh
npx skills update
```

Use these after installing through the skills CLI.

### Claude Code (via plugin marketplace)

Add the marketplace (one-time):

```sh
/plugin marketplace add opanasiuk00/swift-ios-skills
```

Install everything:

```sh
/plugin install all-ios-skills@swift-ios-skills
```

Or install a themed bundle (bundles limit how many skills load into the context window — if you want everything, use `all-ios-skills` above instead of installing multiple bundles):

```sh
/plugin install swiftui-skills@swift-ios-skills
/plugin install swift-core-skills@swift-ios-skills
/plugin install ios-app-framework-skills@swift-ios-skills
/plugin install ios-data-framework-skills@swift-ios-skills
/plugin install ios-ai-ml-skills@swift-ios-skills
/plugin install ios-engineering-skills@swift-ios-skills
/plugin install ios-hardware-skills@swift-ios-skills
/plugin install ios-platform-skills@swift-ios-skills
/plugin install ios-gaming-skills@swift-ios-skills
/plugin install apple-kit-skills@swift-ios-skills
```

### OpenAI Codex

```sh
$skill-installer install https://github.com/opanasiuk00/swift-ios-skills/tree/main/skills/<skill-name>
```

### Claude Web App / Claude Desktop

1. Download the skill folder(s) you want from this repo
2. Zip each skill folder
3. Go to **Settings > Capabilities** and enable "Code execution and file creation"
4. Go to **Customize > Skills**, click **+**, then **Upload a skill**
5. Upload the zip

### ChatGPT

1. Download the skill folder(s) you want from this repo
2. Zip each skill folder
3. Click your profile icon in ChatGPT and select **Skills**
4. Click **New skill** and select **Upload from your computer**
5. Upload the zip

## Quick Start Tutorial

Use this flow when installing the skills for the first time.

### 1. Pick the install method

Use the skills CLI for most agents:

```sh
npx skills add opanasiuk00/swift-ios-skills
```

Use Claude Code plugin bundles if you work in Claude Code:

```sh
/plugin marketplace add opanasiuk00/swift-ios-skills
/plugin install swiftui-skills@swift-ios-skills
```

Use Codex skill installer for one specific skill:

```sh
$skill-installer install https://github.com/opanasiuk00/swift-ios-skills/tree/main/skills/swiftui-patterns
```

### 2. Choose only the skills you need

For a focused setup, install individual skills:

```sh
npx skills add opanasiuk00/swift-ios-skills --skill swiftui-patterns --skill ios-networking
```

For a full local catalog, install everything:

```sh
npx skills add opanasiuk00/swift-ios-skills --all
```

### 3. Verify the install

Ask your agent a task that should trigger an installed skill, for example:

```text
Use the SwiftUI patterns skill to review this @Observable view state.
```

If your agent supports listing installed skills, check that the selected skill
name appears exactly as shown in the [Skills](#skills) table.

### 4. If a skill is missing

1. Check the skill name in the [Skills](#skills) table.
2. Re-run the install command with the exact folder name.
3. Restart the agent or reload its skills if the UI caches capabilities.
4. Run `npx skills check` if you installed through the skills CLI.
5. Reinstall with `npx skills update` when the local copy is stale.

Common causes:

- Typo in the skill name.
- Old renamed skill path.
- Installing a Claude Code bundle when you meant to install a single skill.
- Agent UI did not reload after installation.
- Private fork or GitHub URL is not accessible from the installer.

### 5. Update later

For skills CLI installs:

```sh
npx skills check
npx skills update
```

For Claude Code plugin bundles, reinstall the bundle you use:

```sh
/plugin install swiftui-skills@swift-ios-skills
```

## Plugin Bundles (Claude Code)

| Plugin | Skills included |
|--------|----------------|
| **all-ios-skills** | All 86 skills |
| **apple-kit-skills** | 39 skills spanning Apple Kit frameworks plus CarPlay |
| **swiftui-skills** | focus-engine, swiftui-animation, swiftui-gestures, swiftui-layout-components, swiftui-liquid-glass, swiftui-navigation, swiftui-patterns, swiftui-performance, swiftui-uikit-interop, swiftui-webkit |
| **swift-core-skills** | core-data, swift-api-design-guidelines, ios-architecture, swift-codable, swift-charts, swift-concurrency, swift-formatstyle, swift-language, swift-testing, swiftdata |
| **ios-app-framework-skills** | activitykit, adattributionkit, alarmkit, app-clips, app-intents, avkit, carplay, mapkit, paperkit, pdfkit, photokit, push-notifications, storekit, tipkit, widgetkit |
| **ios-data-framework-skills** | cloudkit, contacts-framework, eventkit, financekit, healthkit, musickit, passkit, weatherkit |
| **ios-ai-ml-skills** | apple-on-device-ai, coreml, natural-language, speech-recognition, vision-framework |
| **ios-engineering-skills** | app-store-optimization, app-store-review, authentication, background-processing, cryptokit, debugging-instruments, device-integrity, ios-accessibility, ios-localization, ios-networking, uikit, vpn, swift-security, swiftlint, ios-simulator, metrickit |
| **ios-hardware-skills** | accessorysetupkit, core-bluetooth, core-motion, core-nfc, dockkit, pencilkit, realitykit, sensorkit |
| **ios-platform-skills** | appmigrationkit, audioaccessorykit, browserenginekit, callkit, cryptotokenkit, energykit, homekit, permissionkit, relevancekit, shareplay-activities |
| **ios-gaming-skills** | gamekit, scenekit, spritekit, tabletopkit |

## Skills

### SwiftUI

| Skill | What it covers |
|-------|---------------|
| [focus-engine](skills/focus-engine/) | @FocusState, defaultFocus, focusSection, focused scene values, focus restoration, UIFocusGuide |
| [swiftui-animation](skills/swiftui-animation/) | Spring animations, PhaseAnimator, KeyframeAnimator, matchedGeometryEffect, SF Symbols |
| [swiftui-gestures](skills/swiftui-gestures/) | Tap, drag, magnify, rotate, long press, simultaneous and sequential gestures |
| [swiftui-layout-components](skills/swiftui-layout-components/) | Grid, LazyVGrid, Layout protocol, ViewThatFits, custom layouts |
| [swiftui-liquid-glass](skills/swiftui-liquid-glass/) | Liquid Glass, glassEffect, GlassEffectContainer, morphing transitions |
| [swiftui-navigation](skills/swiftui-navigation/) | NavigationStack, NavigationSplitView, programmatic navigation, deep linking |
| [swiftui-patterns](skills/swiftui-patterns/) | @Observable, state ownership, environment wiring, view composition, async loading, MV-pattern architecture |
| [swiftui-performance](skills/swiftui-performance/) | Rendering performance, view update optimization, layout thrash, Instruments profiling |
| [swiftui-uikit-interop](skills/swiftui-uikit-interop/) | UIViewRepresentable, UIHostingController, Coordinator, incremental UIKit-to-SwiftUI migration |
| [swiftui-webkit](skills/swiftui-webkit/) | WebView, WebPage, navigation policies, JavaScript calls, local content, custom URL schemes |

### Core Swift

| Skill | What it covers |
|-------|---------------|
| [swift-api-design-guidelines](skills/swift-api-design-guidelines/) | Swift API Design Guidelines -- argument labels, mutating/nonmutating pairs, documentation comments, naming conventions |
| [ios-architecture](skills/ios-architecture/) | iOS architecture patterns: UIKit MVC, MV (@Observable), MVVM, MVI, TCA, Clean Architecture, Coordinator/Router, Repository, SPM modules, decision framework |
| [swift-codable](skills/swift-codable/) | Swift Codable, JSONDecoder, JSONEncoder, CodingKeys, custom decoding, nested JSON |
| [swift-charts](skills/swift-charts/) | Bar, line, area, pie, donut, and 3D charts, scrolling, selection, annotations |
| [swift-concurrency](skills/swift-concurrency/) | Swift concurrency, Sendable, actors, structured concurrency, data-race safety |
| [swift-formatstyle](skills/swift-formatstyle/) | FormatStyle protocol, number/currency/date/duration/measurement formatting, custom styles |
| [swift-language](skills/swift-language/) | Swift language idioms, result builders, property wrappers, typed throws |
| [swift-testing](skills/swift-testing/) | Swift Testing framework, @Test, @Suite, #expect, parameterized tests, mocking |
| [core-data](skills/core-data/) | Core Data persistence, NSPersistentContainer, NSFetchedResultsController, batch operations, staged migration |
| [swiftdata](skills/swiftdata/) | @Model, @Query, #Predicate, ModelContainer, migrations, CloudKit sync, @ModelActor |

### App Experience Frameworks

| Skill | What it covers |
|-------|---------------|
| [activitykit](skills/activitykit/) | ActivityKit, Dynamic Island, Lock Screen Live Activities, push-to-update |
| [adattributionkit](skills/adattributionkit/) | Privacy-preserving ad attribution, postbacks, conversion values, re-engagement |
| [alarmkit](skills/alarmkit/) | AlarmKit system alarms and countdown timers, Lock Screen, Dynamic Island, Live Activities |
| [app-clips](skills/app-clips/) | App Clips, invocation URLs, NFC, QR, App Clip Codes, App Group handoff |
| [app-intents](skills/app-intents/) | App Intents for Siri, Shortcuts, Spotlight, widgets, and Apple Intelligence |
| [avkit](skills/avkit/) | AVPlayerViewController, VideoPlayer, Picture-in-Picture, AirPlay, subtitles |
| [carplay](skills/carplay/) | CarPlay templates, navigation, audio, communication, EV charging apps |
| [mapkit](skills/mapkit/) | MapKit, CoreLocation, annotations, geocoding, directions, geofencing |
| [paperkit](skills/paperkit/) | PaperMarkupViewController, markup editing, drawing, shapes |
| [pdfkit](skills/pdfkit/) | PDFView, PDFDocument, annotations, text search, form filling, thumbnails |
| [photokit](skills/photokit/) | PhotosPicker, AVCaptureSession, photo library, video recording, media permissions |
| [push-notifications](skills/push-notifications/) | UNUserNotificationCenter, APNs, rich notifications, silent push, service extensions |
| [storekit](skills/storekit/) | StoreKit 2 purchases, subscriptions, SubscriptionStoreView, transaction verification |
| [tipkit](skills/tipkit/) | Feature discovery tooltips, contextual tips, tip rules, tip events |
| [widgetkit](skills/widgetkit/) | Home Screen, Lock Screen, and StandBy widgets, Control Center controls, timeline providers |

### Data & Service Frameworks

| Skill | What it covers |
|-------|---------------|
| [cloudkit](skills/cloudkit/) | CKContainer, CKRecord, subscriptions, sharing, CKSyncEngine, SwiftData sync |
| [contacts-framework](skills/contacts-framework/) | CNContactStore, fetch requests, key descriptors, CNContactPickerViewController, save requests |
| [eventkit](skills/eventkit/) | EKEventStore, EKEvent, EKReminder, recurrence rules, EventKitUI editors and choosers |
| [financekit](skills/financekit/) | Apple Card, Apple Cash, Wallet orders, transaction queries, account balances |
| [healthkit](skills/healthkit/) | HKHealthStore, queries, statistics, workout sessions, background delivery |
| [musickit](skills/musickit/) | MusicKit authorization, catalog search, ApplicationMusicPlayer, MPRemoteCommandCenter |
| [passkit](skills/passkit/) | Apple Pay, PKPaymentRequest, PKPaymentAuthorizationController, Wallet passes |
| [weatherkit](skills/weatherkit/) | WeatherService, current/hourly/daily forecasts, alerts, attribution requirements |

### AI & Machine Learning

| Skill | What it covers |
|-------|---------------|
| [apple-on-device-ai](skills/apple-on-device-ai/) | Foundation Models framework, Core ML, MLX Swift, on-device LLM inference |
| [coreml](skills/coreml/) | Core ML model loading, prediction, MLTensor, compute unit configuration, VNCoreMLRequest, MLComputePlan |
| [natural-language](skills/natural-language/) | NLTokenizer, NLTagger, sentiment analysis, language identification, embeddings, Translation |
| [speech-recognition](skills/speech-recognition/) | SpeechAnalyzer, SpeechTranscriber, SFSpeechRecognizer, on-device recognition, audio buffer processing |
| [vision-framework](skills/vision-framework/) | Vision text recognition, face/barcode detection, image segmentation, VisionKit DataScannerViewController |

### iOS Engineering

| Skill | What it covers |
|-------|---------------|
| [app-store-optimization](skills/app-store-optimization/) | ASO keyword strategy, description writing, screenshot optimization, Custom Product Pages, A/B testing |
| [app-store-review](skills/app-store-review/) | App Review guidelines, rejection prevention, privacy manifests, ATT, HIG compliance |
| [authentication](skills/authentication/) | Sign in with Apple, ASAuthorizationController, passkeys, biometric auth (LAContext), credential management |
| [background-processing](skills/background-processing/) | BGTaskScheduler, background refresh, URLSession background transfers |
| [cryptokit](skills/cryptokit/) | SHA-2/SHA-3, HMAC, AES-GCM, ChaChaPoly, HPKE, ML-KEM/ML-DSA, P256/Curve25519 signing, ECDH, Secure Enclave |
| [debugging-instruments](skills/debugging-instruments/) | Xcode debugger, Instruments, os_signpost, MetricKit, crash symbolication |
| [device-integrity](skills/device-integrity/) | DeviceCheck (DCDevice per-device bits), App Attest (DCAppAttestService attestation and assertion flows) |
| [ios-accessibility](skills/ios-accessibility/) | VoiceOver, Dynamic Type, custom rotors, accessibility focus, assistive-technology support |
| [ios-localization](skills/ios-localization/) | String Catalogs, pluralization, FormatStyle, right-to-left layout |
| [ios-networking](skills/ios-networking/) | URLSession async/await, REST APIs, downloads/uploads, WebSockets, pagination, retry, caching |
| [uikit](skills/uikit/) | UIKit lifecycle, Auto Layout, SnapKit, collection views, navigation, animation, memory, concurrency, keyboard, accessibility, SwiftUI interop |
| [vpn](skills/vpn/) | NetworkExtension packet tunnels, TunnelKit, OpenVPN, WireGuard, provider configuration, entitlements, App Groups, debugging |
| [swift-security](skills/swift-security/) | Keychain Services, CryptoKit symmetric/asymmetric, biometric authentication, Secure Enclave, certificate trust, credential storage, OWASP compliance · *Based on [ivan-magda/swift-security-skill](https://github.com/ivan-magda/swift-security-skill)* |
| [ios-simulator](skills/ios-simulator/) | xcrun simctl commands, device lifecycle, push/location/privacy simulation, log streaming, simulator limitations |
| [metrickit](skills/metrickit/) | MXMetricManager, hang diagnostics, crash reports, power metrics |
| [swiftlint](skills/swiftlint/) | SwiftLint setup, .swiftlint.yml, build tool plugin, rule selection, baselines, suppressions, CI integration |

### Hardware & Device Integration

| Skill | What it covers |
|-------|---------------|
| [accessorysetupkit](skills/accessorysetupkit/) | Privacy-preserving BLE/Wi-Fi accessory discovery, ASAccessorySession, picker UI |
| [core-bluetooth](skills/core-bluetooth/) | CBCentralManager, CBPeripheral, BLE scanning/connecting, services, characteristics, background modes |
| [core-motion](skills/core-motion/) | CMMotionManager, CMPedometer, accelerometer, gyroscope, activity recognition, altitude |
| [core-nfc](skills/core-nfc/) | NFCNDEFReaderSession, NFCTagReaderSession, NDEF reading/writing, background tag reading |
| [dockkit](skills/dockkit/) | DockAccessoryManager, camera subject tracking, motor control, framing |
| [pencilkit](skills/pencilkit/) | PKCanvasView, PKDrawing, PKToolPicker, Apple Pencil drawing and annotation |
| [realitykit](skills/realitykit/) | RealityView, entities, anchors, ARKit world tracking, raycasting, scene understanding |
| [sensorkit](skills/sensorkit/) | Research-grade sensor data, ambient light, keyboard metrics, device usage (approved studies) |

### Platform Integration

| Skill | What it covers |
|-------|---------------|
| [appmigrationkit](skills/appmigrationkit/) | Cross-platform data transfer, AppMigrationExtension export/import |
| [audioaccessorykit](skills/audioaccessorykit/) | Audio accessory features, automatic switching, device placement |
| [browserenginekit](skills/browserenginekit/) | Alternative browser engines (EU), process management, web content extensions |
| [callkit](skills/callkit/) | CXProvider, CXCallController, PushKit VoIP registration, call directory extensions |
| [cryptotokenkit](skills/cryptotokenkit/) | TKTokenDriver, TKSmartCard, NFC smart cards, certificate-based auth |
| [energykit](skills/energykit/) | ElectricityGuidance, EnergyVenue, grid forecasts, load event submission, electricity insights |
| [homekit](skills/homekit/) | HMHomeManager, accessories, rooms, actions, triggers, MatterSupport commissioning |
| [permissionkit](skills/permissionkit/) | AskCenter, PermissionQuestion, child communication safety, CommunicationLimits |
| [relevancekit](skills/relevancekit/) | Widget relevance signals, time/location-based relevance providers |
| [shareplay-activities](skills/shareplay-activities/) | GroupActivity, GroupSession, GroupSessionMessenger, coordinated media playback |

### Gaming

| Skill | What it covers |
|-------|---------------|
| [gamekit](skills/gamekit/) | Game Center, GKLocalPlayer, leaderboards, achievements, real-time and turn-based multiplayer |
| [scenekit](skills/scenekit/) | SCNView, SCNScene, 3D geometry, materials, lighting, physics, SceneView |
| [spritekit](skills/spritekit/) | SKScene, SKSpriteNode, SKAction, physics simulation, particle effects, SpriteView |
| [tabletopkit](skills/tabletopkit/) | Multiplayer spatial board games, pieces, cards, dice, Group Activities |

## Structure

Each skill follows the open [Agent Skills](https://agentskills.io) standard:

```
skills/
  skill-name/
    SKILL.md              # Required — instructions and metadata
    references/           # Optional — detailed reference material
      some-topic.md
```

`SKILL.md` contains YAML frontmatter (`name`, `description`) and markdown instructions. The `references/` folder holds longer examples, advanced patterns, and lookup tables that the main file points to.

This repository contains original instructional content and examples for Apple platform development. Where Apple frameworks, APIs, documentation, WWDC sessions, or trademarks are referenced, those materials remain the property of Apple Inc.

This project is not affiliated with or endorsed by Apple Inc.
