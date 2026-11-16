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
- Offer a customisable GUI (planned roadmap feature).

## Documentation
- [Specification](docs/SPECIFICATION.md)
- [Roadmap](ROADMAP.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Technical decisions](docs/DECISIONS.md)

## Status
Project definition and foundation. No application functionality is implemented yet. The first milestone is a persistent project library, scanner, and registration GUI.

## Initial technical direction
Python, PySide6, SQLite, Git/GitHub integrations, and safe Steam shortcut integration. These choices may evolve as implementation research proceeds.