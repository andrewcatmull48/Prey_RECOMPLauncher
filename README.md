# Prey Recomp Launcher

An automation-first library and lifecycle manager for game recompilations on SteamOS/Linux.

**Register once; let the manager handle discovery, updates, executable changes, Proton configuration, and Steam integration.**

## Goals
- Scan selected folders and discover recomp projects, Git repositories, and launchable files.
- Register projects from local installations and Git repository URLs.
- Distinguish prebuilt releases, source projects requiring builds, and manually managed installations.
- Check upstream versions and automate supported updates.
- Rediscover executables after updates, including changed filenames and paths.
- Maintain Steam non-Steam shortcuts without duplicates, including launch paths, arguments, artwork, and Proton settings.
- Launch native Linux binaries natively and configure Proton for Windows executables.
- Preserve saves, game assets, and user configuration; stage updates and roll back failures.
- Deliver a polished, GUI-first desktop application with a deliberate, non-dashboard visual identity.

## Documentation
- [Specification](docs/SPECIFICATION.md)
- [Roadmap](ROADMAP.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Technical decisions](docs/DECISIONS.md)

## Status
Project definition and foundation. No application functionality is implemented yet. Development follows the staged sequence in the roadmap: feet, legs, spine, then head.

## Initial technical direction
Python, PySide6, SQLite, Git/GitHub integrations, and safe Steam shortcut integration. These choices may evolve as implementation research proceeds.

## Final delivery target
The finished application is intended to be distributed as a standalone **AppImage** for SteamOS/Linux. It should open from the desktop/file manager and be straightforward to save/install into the user's local space. Mutable application data must remain outside the read-only AppImage. The exact installation location and desktop integration will be validated on SteamOS.

## Development workflow: Pin and Assess
When a blocker or unsupported feature appears, record the issue and evidence, assess necessity, repair effort, risk and downstream impact, then decide whether to fix it, defer it, or use a simpler maintainable alternative. Verify the chosen path before proceeding.

## Working style
Develop deliberately, one verified step at a time. Prefer GUI workflows and automation. Do not give random or unexplained terminal commands. Every command must have a clear purpose, be minimal and safe, and have its output inspected before the next step. Destructive changes require explicit approval.

## Design direction
- Dark-first, with architecture that can support a future light theme; muted violet accent.
- Persistent left sidebar and spacious library density.
- Small artwork thumbnails, clear typography, fine separators and restrained surfaces rather than a wall of generic cards.
- Combined operational and collection dashboard.
- Library rows keep the main launch action accessible; a contextual three-dot menu provides maintenance actions appropriate to each project.
- Project detail is a workspace with relevant sections such as Overview, Installation, Repository, Build, Steam, History and Settings.
- Screens should suit their task; avoid repeating one generic dashboard/card layout everywhere.
- Visual polish follows working foundations, not placeholder-first design.

## Development sequence
**Feet — Foundation:** app skeleton, database, stable project identity, configuration, logging, migrations, startup/shutdown and early AppImage feasibility validation.

**Legs — Core systems:** scanning, registration, repository/release awareness, update strategies, safe downloads/builds, executable detection and user-data preservation.

**Spine — Integration:** connect discovery, registry, updates, builds, launch detection and Steam; add background work, recovery and rollback.

**Head — GUI:** finish the visual interface around real, tested workflows and data.

Every stage must leave a working, tested deliverable. Do not build on unverified foundations.

## Final roadmap marker
Jess Egg
