# Reflect - Room Correction for macOS

Reflect is a system-wide room correction app for macOS built on driverless CoreAudio Process Taps.

## Current Release

- Latest release: **v0.10.1**
- Distribution format: unsigned DMG
- First launch requires the standard Gatekeeper override

## Requirements

- macOS 14.2 or later
- Apple Silicon or Intel Mac
- REW filter export text file (optional, for EQ correction without measuring)

## Quick Install

1. Download and mount the latest Reflect DMG.
2. Drag `Reflect.app` to **Applications**.
3. Open Reflect via **System Settings → Privacy & Security → Open Anyway**, grant Audio Capture permission, then load filters, choose your output device in Reflect, and press **Start Processing**.

Full install and troubleshooting guide: [INSTALL.md](INSTALL.md)

## Features

- System-wide room correction on macOS
- Built-in **Measure** mode for automatic filter generation
- REW Generic text import and export
- **Correction Strength** control for gentler or stronger correction
- Output-device selection inside Reflect

## Measuring with REW / Importing Filters

Reflect includes a built-in **Measure** mode for automatic room correction. If you prefer to measure in Room EQ Wizard and import filters manually, see [Measuring with REW and Importing Filters](REW.md).

## Migration and Rollback

If you previously used the old driver-based build, use the migration guide in the `roomcorrector` source repository:

- [Migration and rollback](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/MIGRATION.md)

## Known Limitations

- Unsigned build — first-launch Gatekeeper override required.
- No automatic updates.
- No per-app routing.
- No convolution / IR processing.

## What's New in v0.10.1

### Reliability

- Improved repeated output switching while processing is active
- Better recovery when external devices are connected or re-enumerated
- Fixed in-app FAQ links for measurement help

## Recent Improvements

- Built-in measurement and Auto-EQ workflow
- REW import and export from **Correct** mode
- Correction Strength slider for quick tuning
- Unified help, settings, and FAQ surface in the app

## Source code and build docs

This repository is the public release surface for Reflect. Source code, architecture notes, and build instructions live in **[mbaumannn/roomcorrector](https://github.com/mbaumannn/roomcorrector)**:

- [Architecture](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/ARCHITECTURE.md)
- [Measurement pipeline PRD](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/PRD-python-experiments-into-Reflect.md)

## Feedback

Report issues via GitHub Issues and include:

- macOS version
- Device/output hardware
- What you expected vs what happened
- Relevant Console logs (filter on `Reflect`)
