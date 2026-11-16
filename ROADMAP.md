# Roadmap

Development is intentionally staged as **feet → legs → spine → head**. Each stage must produce a working, verified result before the next becomes its focus.

## Feet — Foundation
- [ ] Establish the Python/PySide6 application skeleton and startup/shutdown lifecycle.
- [ ] Implement SQLite persistence, schema migrations, and stable project UUIDs.
- [ ] Add per-user configuration, logging, diagnostics, and error handling.
- [ ] Validate the AppImage/Qt packaging route early on SteamOS; do not leave packaging feasibility until the end.
- [ ] Establish automated tests and a repeatable development/build environment.
- [ ] Add a minimal GUI shell sufficient to exercise the foundation.

**Exit test:** create and save project records, close/reopen the app, and verify data persists without corruption. Confirm the packaging approach is viable on the target platform.

## Legs — Core systems
- [ ] Read-only scanning of configured locations with depth and exclusion controls.
- [ ] Detect Git repositories, recomp/build markers, and ELF, shell, and PE executables.
- [ ] Group related files into candidates; never register every executable independently.
- [ ] Manual registration, editing, ignoring and removal from the library.
- [ ] Repository URL validation and Git metadata tracking.
- [ ] GitHub release/commit awareness and project-specific asset selection.
- [ ] Explicit strategies for prebuilt releases, source builds and manual tracking.
- [ ] Safe staged downloads/extraction; prevent archive traversal and unsafe symlinks.
- [ ] Explicit, trusted build recipes with logs and dependency checks.
- [ ] Executable rediscovery after updates/builds, including changed names and paths.
- [ ] Preserve saves, settings, original game assets and user-managed files.
- [ ] Keep known-good versions and support rollback.

**Exit test:** manage at least one real project through registration and its supported update or rebuild path, rediscover its executable, and preserve user data.

## Spine — Integration
- [ ] Connect scanner, project registry, repository tracker, update orchestrator, build runner and executable detector.
- [ ] Implement a durable background job queue and progress/reporting model.
- [ ] Connect launch configuration, native Linux launch and per-project Proton handling.
- [ ] Research and implement safe Steam non-Steam shortcut reconciliation.
- [ ] Preserve shortcut identity where supported and prevent duplicates.
- [ ] Update the matching shortcut when an executable changes; leave unrelated Steam entries untouched.
- [ ] Add transaction boundaries, recovery, rollback and useful activity history.
- [ ] Test the full lifecycle end-to-end with representative projects.

**Exit test:** a project can be discovered, registered, checked, updated or built, launched, and reconciled with Steam without manually joining the systems together.

## Head — Finished GUI and experience
- [ ] Complete the polished desktop interface around the real underlying workflows.
- [ ] Persistent left sidebar; spacious library rows with small artwork.
- [ ] Keep the primary launch action visible and provide a contextual three-dot menu per row.
- [ ] Contextual menu actions may include Check for updates, Open containing folder, Manage project, View logs, Rebuild where supported, and Remove from library.
- [ ] Removing a project unregisters it only; it must never silently delete project files.
- [ ] Combined operational and collection dashboard: useful activity, project status, recent work and actionable issues.
- [ ] Project detail workspace with relevant Overview, Installation, Repository, Build, Steam, History and Settings sections; hide irrelevant capabilities.
- [ ] Discovery/registration, update queue, activity/history and settings each get layouts suited to their purpose.
- [ ] Search, filters, sorting and persisted UI preferences.
- [ ] Dark-first theme with muted violet accent; architecture supports a future light theme.
- [ ] Subtle transitions, restrained surfaces, clear status text and meaningful icons.
- [ ] Validate keyboard, mouse, handheld desktop-mode and accessibility basics.

**Exit test:** the full application is understandable and comfortable to use without requiring the user to understand Git, CMake, Ninja, executable paths, Proton prefixes or Steam shortcut internals.

## Final delivery and acceptance
- [ ] Produce a standalone SteamOS/Linux AppImage.
- [ ] Open it from the desktop/file manager and provide a simple user-space save/install path.
- [ ] Keep mutable state in writable per-user locations, not inside the AppImage.
- [ ] Confirm desktop integration and installation location through SteamOS testing.
- [ ] Reproducible packaging, upgrade path, documentation and final regression tests.
- [ ] Verify backup/restore and ensure manager updates do not overwrite managed games or user data.

## Delivery principles
1. Prefer automation and sensible defaults over repeated prompts.
2. Ask only when a genuine ambiguity or risk cannot be resolved automatically.
3. Scanning is read-only; never move, rename, delete or modify discovered files.
4. Never overwrite saves, user configuration or original game assets during routine updates.
5. Stage and validate updates; retain rollback capability.
6. Preserve unrelated Steam entries and settings.
7. Use project definitions/recipes for special cases instead of hardcoding games into the app.
8. Never execute arbitrary downloaded build scripts without an explicit trusted project build configuration.
9. Do not identify projects by executable name or path; use stable UUIDs.
10. Do not build later stages on untested foundations.

## Pin and Assess process
When a blocker, missing capability, or unexpectedly difficult integration is encountered:
1. **Pin** — record the issue, relevant logs/output, affected feature and what was attempted.
2. **Assess** — determine whether it is essential now, likely repair effort, technical risk and downstream impact.
3. **Choose** — fix now, defer with a clear note, or select a simpler reliable alternative.
4. **Protect** — choose the least fragile maintainable path without compromising data safety, project identity or future compatibility.
5. **Verify** — test the selected approach and record the decision before proceeding.

No speculative commands or random trial-and-error. Commands must be purposeful, explained, minimal and validated against actual output. Prefer GUI workflows and automate repetitive setup, testing and packaging.

## Final roadmap marker
Jess Egg
