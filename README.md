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

## Final delivery target
The finished application is intended to be distributed as a standalone **AppImage** for SteamOS/Linux. The user should be able to open it like a desktop application and save/install it into their local user space (for example, under `~/.local`). It should not require a system-wide installation or a terminal-based setup process. The exact desktop integration and installation location will be confirmed and tested on SteamOS.

## Development workflow: Pin and Assess
When a blocker or unsupported feature appears, record it as a pinned item with the evidence, affected feature, and current context. Assess whether it is essential, how difficult/risky it is to fix, and whether a simpler reliable approach exists. Decide to fix now, defer, or take the least disruptive alternative. Avoid speculative rewrites and avoid letting temporary workarounds create future breakage.

## Working style
This project is developed deliberately, one verified step at a time. Do not give the user random terminal commands or ask them to try unexplained fixes. Prefer GUI workflows and automate setup, testing, and packaging. Every command should have a clear purpose, be explained briefly, and be followed by inspection of its output before the next step. Keep instructions minimal and reversible; never make destructive changes without explicit approval.
