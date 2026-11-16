# Architecture Proposal

This records the initial direction and should evolve with implementation research. Implementation follows feet → legs → spine → head; later layers must not be built on unverified foundations.

## Principles
- Stable project UUIDs independent of names/paths.
- Separate metadata from installed files and user data.
- Reusable services rather than game-specific GUI logic.
- Explicit update strategies for different distribution models.
- Non-destructive discovery and staged updates.
- Steam integration scoped to the matching project shortcut.
- GUI customisation separated from business logic.
- Every milestone leaves a working, tested deliverable.
- Keep mutable app state separate from the distributable AppImage.

## Proposed layers
```text
PySide6 desktop GUI
    |
Application / orchestration services
    |
    +-- Project registry
    +-- Library scanner
    +-- Repository/release tracker
    +-- Update orchestrator
    +-- Archive/staging manager
    +-- Build runner
    +-- Executable detector
    +-- Launch configuration manager
    +-- Proton manager
    +-- Steam shortcut manager
    +-- Background job queue / notifications
    |
Domain models + SQLite
    |
Filesystem + Git/GitHub + Steam
```

## Suggested package layout
```text
src/prey_recomp_launcher/
  app.py
  config/
  database/
  domain/
    models.py
    enums.py
  services/
    library_scanner.py
    project_registry.py
    repository_tracker.py
    release_provider.py
    update_orchestrator.py
    archive_manager.py
    build_runner.py
    executable_detector.py
    launch_manager.py
    proton_manager.py
    steam_manager.py
  integrations/
    git/
    github/
    steam/
  ui/
    main_window.py
    views/
    dialogs/
    widgets/
    themes/
  workers/
tests/
docs/
```

## Core entities
### Project
Persistent UUID, display data, install roots, source repository, update strategy, installed version, launch target, executable platform, Proton configuration, Steam association, data paths and status.

### Update strategy
- `release_asset`: download an upstream prebuilt release.
- `git_build`: update source and run an explicitly configured build recipe.
- `manual`: track local project and upstream information without automatic installation.

### Launch target
Prefer a path relative to the managed install root. Store platform, working directory, arguments and environment. Resolve absolute paths when needed.

### Steam association
Map project UUID to a stable Steam non-Steam shortcut identity. Research Steam app ID/shortcut behaviour and compatibility settings before implementation.

## Update transaction
1. Check upstream version and update strategy.
2. Prepare staging.
3. Download/fetch source.
4. Verify available integrity metadata.
5. Extract/build.
6. Discover executable and required files.
7. Validate candidate installation.
8. Record current known-good state.
9. Activate new payload.
10. Reconcile Steam target and metadata.
11. Record success/history.
12. On failure, restore previous application state and Steam target.

Persistent user data should live outside replaceable application payloads wherever possible.

## Git source handling
Do not unconditionally pull into arbitrary user directories. Prefer manager-controlled source working trees or a defined strategy for existing repositories. Detect local modifications. Build commands must be explicit, inspectable and attached to trusted project configuration.

## Steam integration research
Before writing Steam config, confirm current SteamOS shortcut format, non-Steam app ID generation and identity preservation, compatibility tool storage, artwork paths/naming and safe behaviour while Steam is running. Back up and atomically replace modified files. Test that unrelated entries remain unchanged.

## Feet — Foundation architecture
Build the app entry point, configuration and logging, SQLite schema/migrations, domain models and stable UUID registry first. Validate startup/shutdown and persistence. Prove the PySide6/Qt packaging route and AppImage feasibility on SteamOS early. Keep the first GUI minimal; its purpose is to exercise and verify the foundation.

## Legs — Core service architecture
Implement scanner, registration, repository/release providers, strategy interface, staged update engine, build runner and executable detector as separable services. Use explicit project recipes and a clear boundary between replaceable application payloads and persistent user data. Scanner stays read-only. Build execution is configured and inspectable rather than inferred from arbitrary scripts.

## Spine — Orchestration and integration
Connect services through an orchestration layer and durable background jobs. Model progress, cancellation, errors and recovery explicitly. Connect launch configuration, Proton selection and Steam shortcut reconciliation only after the relevant format and behaviour research. Use transactions/backups and preserve unrelated Steam data. Exercise full lifecycle paths end-to-end.

## Head — Presentation architecture
The GUI consumes application/domain services; business logic must not live in widgets. Keep navigation, library rows, contextual actions, project workspace, dashboard and operational views distinct. Design around real service states and operations rather than placeholder metrics. Use a persistent left sidebar, spacious list-first library, small thumbnails, dark-first theme and muted violet accent. Theme tokens should make a future light theme possible. Prefer restrained surfaces and fine separators over repeated cards.

## AppImage and user-space delivery
The final release is a standalone Linux AppImage. It should run when opened from the desktop/file manager and offer a straightforward way to save/install a copy into the user's local space. Keep the image immutable and mutable state in standard per-user writable locations. Keep project installations, source trees and game data at configured locations; never bundle or relocate them into the AppImage. Select packaging tools after validating PySide6/Qt runtime compatibility and SteamOS behaviour. Packaging is reproducible and tested as part of release acceptance.

## Blocker management: Pin and Assess
Capture reproduction context, evidence, affected milestone, requirement criticality, estimated effort, technical risk and downstream effects. Choose fix-now, defer, or a maintainable alternative. Prefer the simplest supported path that preserves data safety and future compatibility. Do not hide blockers behind unexplained workarounds.

## User-facing development procedure
Avoid random terminal trial-and-error. Commands should be deliberate, explained, minimal and followed by inspection of output before the next step. Prefer GUI workflows and automate repeatable setup, testing and packaging. Destructive changes require explicit user approval.

## Final roadmap marker
Jess Egg
