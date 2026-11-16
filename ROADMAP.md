# Roadmap

## Phase 1 — Foundation and library
- [ ] Python application structure and PySide6 GUI.
- [ ] SQLite persistence with stable project UUIDs.
- [ ] Configurable scan locations and read-only discovery.
- [ ] Detect Git repositories, recomp markers, and ELF, shell, and PE executables.
- [ ] Manual project registration and editing.
- [ ] Library view with location, executable, platform, and status.

**Milestone:** Scan directories, review and register candidates, and retain the library across launches.

## Phase 2 — Repository and release awareness
- [ ] Accept and validate Git URLs; detect repository metadata and branch.
- [ ] Check GitHub releases and select assets using project rules.
- [ ] Track source commits, installed version, and latest upstream version.
- [ ] Display release notes/commit summaries and update strategy.

## Phase 3 — Automated updates
- [ ] Download release assets and verify checksums where available.
- [ ] Safely extract to staging; prevent archive path traversal.
- [ ] Update source working trees and run configured build recipes.
- [ ] Separate replaceable application files from saves, settings, and game assets.
- [ ] Validate before activation; roll back failed updates.
- [ ] Maintain logs and update history.

## Phase 4 — Executable and launch management
- [ ] Discover executables after install/update/build.
- [ ] Distinguish Linux binaries/scripts from Windows PE files.
- [ ] Track launch targets relative to managed roots where possible.
- [ ] Detect renamed/relocated executables and update launch targets.
- [ ] Maintain arguments, working directory, and environment.

## Phase 5 — Steam and Proton
- [ ] Create non-Steam shortcuts associated with stable project UUIDs.
- [ ] Detect and update existing entries without duplicates.
- [ ] Update executable path, arguments, working directory, artwork, and metadata.
- [ ] Detect installed Proton versions and configure per-project compatibility.
- [ ] Launch native Linux projects natively; configure Proton for Windows executables.
- [ ] Preserve unrelated Steam entries/settings using backups and safe writes.

## Phase 6 — Background automation
- [ ] Scheduled repository/release checks and update queue.
- [ ] Background downloads and configurable notify/download/install policies.
- [ ] Notifications and SteamOS-friendly background integration.

## Phase 7 — GUI customisation
- [ ] Themes, including dark mode.
- [ ] Card/list layouts, adjustable panels, sorting, filtering, and grouping.
- [ ] Custom artwork and metadata.
- [ ] Configurable dashboard/widgets and persisted UI preferences.

## Phase 8 — Reliability and polish
- [ ] Dependency detection, diagnostics, and project health checks.
- [ ] Backup/restore and import/export project definitions.
- [ ] Packaging, documentation, and tests with representative projects.

## Delivery principles
1. Prefer automation and sensible defaults over repeated prompts.
2. Ask only when a genuine ambiguity or risk cannot be resolved automatically.
3. Never overwrite saves, user configuration, or original game assets during routine updates.
4. Stage and validate updates; retain rollback capability.
5. Preserve unrelated Steam entries and settings.
6. Use project definitions/recipes for special cases instead of hardcoding games into the app.
