# Reflect - Room Correction for macOS

Reflect is a system-wide room correction app for macOS using driverless CoreAudio Process Taps.

## Status

Reflect v2 is in pre-release testing and uses an app-only install flow.
Current test release: **v1.0.0-beta5**.

## Requirements

- macOS 14.2 or later
- Apple Silicon or Intel Mac
- REW filter export text file (optional, for EQ correction)

## Quick Install (3 steps)

1. Download and mount the latest Reflect DMG.
2. Install `Reflect.app`:
   - Easiest for testers: run `Install Reflect.command` (copies app + clears quarantine), or
   - Manual: drag `Reflect.app` to `/Applications`.
3. Launch Reflect, grant Audio Capture permission, press **Start Processing**.

Detailed steps: [INSTALL.md](INSTALL.md)

## REW Workflow

To create and export filters from Room EQ Wizard, see [REW.md](REW.md).

## Migration and Rollback

If you previously used the legacy driver build, use the migration guide in the source repository:

- Migration + rollback guide: [roomcorrector/Docs/MIGRATION.md](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/MIGRATION.md)

## Current Known Limitations (Pre-release)

- Unsigned beta builds may require first-launch Gatekeeper override (right-click -> Open).
- No automatic updates yet.
- No per-app routing.
- No IR convolution in the v2 runtime.

## Build / Source Docs

Reflect source code, architecture docs, and build instructions live in the private development repository:

- Source + build docs: [roomcorrector](https://github.com/mbaumannn/roomcorrector)
- v2 architecture: [Docs/ARCHITECTURE.md](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/ARCHITECTURE.md)
- v2 execution checklist: [Docs/TODO.md](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/TODO.md)

## Feedback

Report issues via GitHub Issues and include:

- macOS version
- Device/output hardware
- What you expected vs what happened
- Relevant Console logs (filter on `Reflect`)
