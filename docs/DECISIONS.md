# Technical Decisions

## 2026-11-16 — Initial project definition

### Automation-first recomp lifecycle manager
The application manages the full lifecycle of recomp projects: discover, register, track upstream, update/build, rediscover executables, and keep Steam launch configuration correct. The library is the user-facing control surface, not the whole product.

### Stable project identity
Each registered project has an internal UUID. The UUID links persistent metadata and Steam shortcuts; executable names and paths can change.

### Distinct update strategies
Prebuilt releases, source repositories requiring builds, and manually managed projects use distinct strategies behind a common update orchestrator.

### Steam path reconciliation is core
When an update changes an executable filename or directory, update the manager's launch target and matching Steam non-Steam shortcut automatically. Do not create duplicates.

### Platform-aware launch
Native Linux projects launch natively. Windows executables use an appropriate per-project Proton configuration.

### Preserve and recover
Stage and validate updates before activation. Preserve saves, settings, original game assets, and user-managed data. Retain a known-good version and roll back failed updates where possible.

### GUI customisation is on the roadmap
Themes, layouts, adjustable panels, and configurable library views are planned after the core library and automation.


## 2026-11-16 — Delivery and development workflow clarification

### Final distributable is an AppImage
The completed application should be delivered as a standalone SteamOS/Linux AppImage. It should open from the desktop/file manager and be savable/installed into the user's local space (likely under `~/.local`; exact location and desktop integration are to be validated). Mutable state belongs in writable per-user locations, not inside the AppImage.

### Pin and Assess is the blocker policy
When a blocker appears, pin it with evidence and context, assess necessity, repair effort, risk, and future impact, then choose fix now, defer, or a simpler maintainable alternative. Prefer the path of least resistance without creating fragile workarounds or future issues.

### No speculative terminal troubleshooting
The user does not want random commands hoping they fix something. Commands must be purposeful, explained, minimal, and validated against output before continuing. Prefer GUI workflows and automate setup, diagnostics, builds, and packaging. Destructive actions require explicit approval.
