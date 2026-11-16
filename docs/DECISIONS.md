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
