# Functional Specification

## Purpose
Prey Recomp Launcher is a personal GUI application for managing recompilation projects on SteamOS/Linux. It manages discovery, registration, upstream tracking, updating/building, executable management, and Steam integration. It is an automation engine presented through a library GUI, not merely a static launcher.

## Core workflow
1. Scan configured directories or accept a Git repository URL.
2. Discover project metadata, installation files, update model, and launchable executable.
3. Register once and assign a stable internal UUID.
4. Track the upstream repository/release.
5. Apply supported release downloads or source updates/builds.
6. Rediscover the executable even if its name or path changes.
7. Reconcile the existing Steam shortcut, retaining its identity and configuration.
8. Update installed version, health, and history.

Manual interaction should be limited to genuine ambiguity, missing project-specific instructions, or risks to existing data.

## Platform and technology
- Primary target: Steam Deck / SteamOS desktop mode.
- Initial language: Python; GUI: PySide6; persistence: SQLite.
- Source control: Git CLI; upstream metadata: GitHub API initially.
- Steam integration: format-aware management of local non-Steam shortcuts.
- Linux executables launch natively; Windows PE executables use an appropriate Proton tool.
These are initial choices and may evolve after implementation research.

## Discovery and registration
Scan user-configured roots with configurable depth/exclusions. Detect Git trees and common project markers (CMake, Ninja, Meson, Makefiles, manifests), plus ELF/Linux binaries, shell scripts, and Windows PE executables. Group related files into candidates rather than registering every executable separately.

Scanning is read-only: it must not move, rename, delete, or modify discovered files. Candidates remain unregistered until accepted or ignored. Registration can start from a local directory, a Git URL, or both.

## Stable project metadata
Every project receives a persistent UUID; filenames and directories are not identities. Store at least:
- UUID, display name, description, installation/root paths.
- Repository URL/provider/branch; installed commit/version and latest upstream release/commit.
- Update strategy and release asset selection rules.
- Executable path/detection metadata, platform, working directory, arguments, environment.
- Proton requirement/tool and Steam shortcut association.
- Artwork, save/configuration/user-data locations, build recipe/dependencies.
- Check/update timestamps, health/status, last error, and update history.

Project definitions should be exportable without bundling copyrighted game data, secrets, or machine-specific state.

## Update strategies

### Prebuilt release
Query upstream release metadata, select the correct platform/architecture asset using project rules, download it, verify checksums/signatures when provided, and extract to staging with archive traversal protection. Identify the executable and required payload, then activate only after validation.

### Source repository requiring a build
Track the configured remote and branch/tag, fetch and detect changes, update a manager-controlled source working tree or use a defined safe strategy for an existing repository, detect local modifications, account for submodules/Git LFS/dependencies where configured, run an explicit build recipe, capture logs, and retain previous known-good builds. Do not assume a simple git pull is safe or sufficient.

### Manually managed
Track local installation and optional upstream information, but do not invent an update workflow.

### Update policy
Support notify-only, automatic download, and automatic installation for validated workflows. Avoid unnecessary confirmation prompts.

## Safe updates and rollback
Download/extract/build in staging. Reject archive paths escaping the extraction root. Keep persistent user data outside replaceable application payloads where possible. Preserve saves, settings, original game assets, and source archives. Validate before activation, retain the previous known-good state, roll back failed activation/validation, and log actions. Routine updates must not delete original game dumps or user-managed files.

## Executable discovery and reconciliation
Executable names and paths may change across releases. Do not identify projects by executable filename alone. Discover candidates after each update/build; use project metadata, release manifests, file types, and prior launch configuration. Prefer storing paths relative to the managed install root. Resolve current absolute paths at launch/reconciliation time. Update the launch target and Steam entry automatically when a new executable is identified. If several targets are equally plausible, use project rules or request a one-time selection.

## Steam integration
Create non-Steam shortcuts associated with stable project UUIDs. Detect/reuse existing entries; avoid duplicates. Update executable path, working directory, launch arguments, artwork, and compatibility settings while preserving unrelated entries and fields.

After an update changes the executable: discover it, update the project launch target, find the matching existing Steam shortcut, update its target/path while preserving identity where supported, and record the result.

Before implementing writes, research SteamOS shortcut format, non-Steam app ID handling, compatibility tool storage, artwork locations/naming, and concurrency while Steam is running. Use a parser/writer, backups, and atomic replacement. Never overwrite unrelated shortcuts or settings.

## Proton and platform handling
Identify native Linux binary/script versus Windows PE executable. Do not force Linux projects through Proton. Detect installed Proton versions including Proton Experimental and GE-Proton. Support per-project tool and compatibility prefix where appropriate. Preserve launch arguments, environment, and working directory. Define a fallback if the selected Proton tool is missing and report it.

## GUI
Planned views: Library, Project Detail, Discovery/Registration, Update Queue/History, Build/Diagnostic Logs, and Settings. GUI customisation is planned after core library and automation: themes, layouts, card/list views, adjustable panels, sorting/filtering, custom artwork, and configurable dashboard widgets. Sensible defaults should minimise setup.

## Automation defaults
Automate scheduled upstream checks, update detection, known asset selection, downloads/extraction, configured builds, executable rediscovery, Steam shortcut repair, unambiguous Proton assignment, and version/status/history updates.
Ask only when asset selection is ambiguous, build instructions/dependencies are unknown, executable candidates are equally plausible, existing data may be overwritten, or a project-specific choice cannot be inferred safely.

## Security and reliability
Treat repository metadata, release assets, archives, and build scripts as untrusted. Do not execute arbitrary downloaded scripts without an explicit trusted project build configuration. Validate origins/checksums where available. Protect against archive traversal and unsafe symlinks. Do not put secrets in project files/logs. Use backups, atomic operations, and an audit trail.

## Initial non-goals
- Automatic support for every recomp project immediately.
- Universal build recipes without project-specific instructions.
- Cloud syncing local game data.
- Managing or downloading copyrighted game dumps/assets.
- Replacing Steam as the runtime/library.

The first milestone is a reliable local scanner, persistent library, and registration GUI.
