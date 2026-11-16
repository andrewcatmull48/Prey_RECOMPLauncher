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


## Final packaging and installation requirement
- [ ] Produce a standalone SteamOS/Linux AppImage as the final distributable.
- [ ] Ensure it launches by opening the AppImage from the desktop/file manager.
- [ ] Provide a simple option to save/install it into the user's local space (target such as `~/.local`, exact location to be validated).
- [ ] Keep application data/configuration in appropriate per-user locations, separate from the AppImage itself.
- [ ] Test desktop integration and launch behaviour on SteamOS.
- [ ] Avoid requiring users to run a sequence of terminal commands to install or operate the application.

## Pin and Assess process
When a blocker, missing capability, or awkward integration is encountered:
1. **Pin** — record the issue, relevant logs/output, affected feature, and what was being attempted.
2. **Assess** — determine whether it is required now, its likely repair effort, technical risk, and downstream impact.
3. **Choose** — fix now, defer with a clear note, or select a simpler reliable alternative.
4. **Protect** — prefer the path of least resistance that does not create fragile workarounds or future architectural problems.
5. **Verify** — test the chosen approach before proceeding and record the decision.

The user should not be sent random commands to see whether something works. Commands must be purposeful, explained, minimal, and validated against their output. Prefer GUI operations and automate repetitive setup/build/package tasks.
