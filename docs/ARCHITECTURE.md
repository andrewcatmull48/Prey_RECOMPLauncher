# Architecture Proposal

This records the initial direction and should evolve with implementation research.

## Principles
- Stable project UUIDs independent of names/paths.
- Separate metadata from installed files and user data.
- Reusable services rather than game-specific GUI logic.
- Explicit update strategies for different distribution models.
- Non-destructive discovery and staged updates.
- Steam integration scoped to the matching project shortcut.
- GUI customisation separated from business logic.

## Proposed layers

```text
PySide6 GUI
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
    +-- Notification scheduler
    |
SQLite + filesystem + Git/GitHub + Steam
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
Persistent UUID, display data, install roots, source repository, update strategy, installed version, launch target, executable platform, Proton configuration, Steam association, data paths, and status.

### Update strategy
- `release_asset`: download an upstream prebuilt release.
- `git_build`: update source and run an explicitly configured build recipe.
- `manual`: track local project and upstream information without automatic installation.

### Launch target
Prefer a path relative to the managed install root. Store platform, working directory, arguments, and environment. Resolve absolute paths when needed.

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
Do not unconditionally pull into arbitrary user directories. Prefer manager-controlled source working trees or a defined strategy for existing repositories. Detect local modifications. Build commands must be explicit, inspectable, and attached to trusted project configuration.

## Steam integration research
Before writing Steam config, confirm current SteamOS shortcut format, non-Steam app ID generation and identity preservation, compatibility tool storage, artwork paths/naming, and safe behaviour while Steam is running. Back up and atomically replace modified files. Test that unrelated entries remain unchanged.

## Initial build sequence
1. SQLite model and migration mechanism.
2. Read-only scanner for configured folders.
3. Manual registration and library GUI.
4. Repository URL parsing and Git metadata.
5. Release/commit checking.
6. Update strategy interface and one release-asset workflow.
7. Executable detection and launch target model.
8. Steam integration after format research.


## AppImage and user-space delivery
The final release is a standalone Linux AppImage. The application should run when opened from the desktop/file manager and offer a straightforward way to save/install a copy into the user's local space. Keep the AppImage immutable and keep mutable state in standard per-user writable locations. Keep project installations, source trees, and game data at their configured locations; never bundle or relocate them into the AppImage. Select the packaging toolchain after validating PySide6/Qt runtime compatibility and SteamOS behaviour. Packaging must be reproducible and tested as part of release acceptance.

## Blocker management: Pin and Assess
Use a lightweight issue record for blockers encountered during development. Capture reproduction context, evidence, affected milestone, requirement criticality, estimated effort, technical risk, and possible downstream effects. Choose among fix-now, defer, or a maintainable alternative. Prefer the simplest supported path that preserves data safety and future compatibility. Do not hide a blocker behind an unexplained workaround.

## User-facing development procedure
Avoid random terminal trial-and-error. Commands should be deliberate, explained, minimal, and followed by inspection of output before the next step. Prefer GUI workflows and automate repeatable setup, testing, and packaging. Destructive changes require explicit user approval.
