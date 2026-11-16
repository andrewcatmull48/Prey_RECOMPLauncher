# Technical Decisions

## 2026-11-16 — Initial project definition

### Automation-first recomp lifecycle manager
The application manages the full lifecycle of recomp projects: discover, register, track upstream, update/build, rediscover executables and keep Steam launch configuration correct. The library is the user-facing control surface, not the whole product.

### Stable project identity
Each registered project has an internal UUID. The UUID links persistent metadata and Steam shortcuts; executable names and paths can change.

### Distinct update strategies
Prebuilt releases, source repositories requiring builds, and manually managed projects use distinct strategies behind a common update orchestrator.

### Steam path reconciliation is core
When an update changes an executable filename or directory, update the manager's launch target and matching Steam non-Steam shortcut automatically. Do not create duplicates.

### Platform-aware launch
Native Linux projects launch natively. Windows executables use an appropriate per-project Proton configuration.

### Preserve and recover
Stage and validate updates before activation. Preserve saves, settings, original game assets and user-managed data. Retain a known-good version and roll back failed updates where possible.

## 2026-11-16 — Delivery and development workflow

### Final distributable is an AppImage
The completed application should be delivered as a standalone SteamOS/Linux AppImage. It should open from the desktop/file manager and be savable/installed into the user's local space. Exact location and desktop integration require SteamOS validation. Mutable state belongs in writable per-user locations, not inside the AppImage.

### Pin and Assess is the blocker policy
When a blocker appears, pin it with evidence and context, assess necessity, repair effort, risk and future impact, then choose fix now, defer, or a simpler maintainable alternative. Prefer the path of least resistance without creating fragile workarounds or future issues.

### No speculative terminal troubleshooting
Commands must be purposeful, explained, minimal and validated against output before continuing. Prefer GUI workflows and automate setup, diagnostics, builds and packaging. Destructive actions require explicit approval.

## 2026-11-16 — Staged delivery and experience direction

### Feet, legs, spine, head
Development is deliberately staged. Feet establishes a persistent, testable foundation and validates packaging feasibility. Legs delivers the core discovery, registration, repository, update/build and executable systems. Spine integrates the systems into a complete lifecycle including launch and Steam. Head completes the polished GUI around real, verified workflows. Each stage must have an exit test and leave a working deliverable.

### GUI is a desktop application, not a web dashboard
Use a persistent left sidebar, spacious list-first library, small artwork thumbnails, dark-first styling and muted violet accent. Keep surfaces restrained, use clear typography and fine separators, and avoid repetitive generic card layouts. The dashboard combines operational and collection information. Library rows keep launch accessible and provide contextual maintenance actions through a three-dot menu. Removing from the library unregisters only; it never deletes project files. Project details are organised as a relevant workspace, not a fixed set of irrelevant tabs.

### Design follows working foundations
Do not spend early effort polishing placeholder screens or prematurely finalising every visual detail. Establish real domain data and service workflows first, then complete the interface against actual states and operations.

### Packaging feasibility is tested early
AppImage remains the final distribution target, but Qt/runtime and SteamOS compatibility must be validated during the foundation stage. Do not defer all packaging risk to the end.

### Final roadmap marker
Jess Egg
