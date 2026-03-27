# Reflect - Room Correction for macOS

Reflect is a system-wide room correction app for macOS using driverless CoreAudio Process Taps.

## Status

Reflect v2 is in pre-release testing and uses an app-only install flow.
Current test release: **v1.0.0-beta9** (Quality Stabilization V1 plus measurement UI cleanup: recovery/sample-rate hardening, latency reporting, safer filter transitions, soft limiter, multi-sweep measurement, and a cleaner **Measure** workflow with inline advanced sections, FAQ deep links, and footer tooltip fixes).

## Requirements

- macOS 14.2 or later
- Apple Silicon or Intel Mac
- REW filter export text file (optional, for EQ correction)

## Quick Install (3 steps)

1. Download and mount the latest Reflect DMG.
2. Install `Reflect.app`:
   - Easiest for testers: run `Install Reflect.command` (copies app + clears quarantine), or
   - Manual: drag `Reflect.app` to `/Applications`.
3. Launch Reflect, grant Audio Capture permission. Load filters (**Correct** mode: import icon → REW Generic text, or **Measure** mode: complete a run and **Apply Filters**), pick your output, then press **Start Processing**.

Detailed steps: [INSTALL.md](INSTALL.md)

## REW Workflow

To create and export filters from Room EQ Wizard, see [REW.md](REW.md).

## Migration and Rollback

If you previously used the legacy driver build, use the migration guide in the **roomcorrector** source repository:

- [Migration and rollback](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/MIGRATION.md)

## Current Known Limitations (Pre-release)

- Unsigned beta builds may require first-launch Gatekeeper override (right-click -> Open).
- No automatic updates yet.
- No per-app routing.
- No IR convolution in the v2 runtime.

## What's New in beta9

- Quality Stabilization V1 from [roomcorrector PR #29](https://github.com/mbaumannn/roomcorrector/pull/29): headroom / auto-preamp, REW shelf parity validation, sample-rate reapply, runtime recovery hardening, anti-click filter transitions, post-EQ soft limiter, latency reporting, multi-sweep averaging, level check, and Auto-EQ alignment/refinement improvements.
- Measurement UI cleanup from [roomcorrector PR #31](https://github.com/mbaumannn/roomcorrector/pull/31): inline **Capture Options** and **Target & Analysis Options**, dedicated FAQ tab with deep links, better footer tooltip behavior, cleaner button hierarchy, and more stable popover layout.
- Packaging remains app-only: DMG includes `Reflect.app`, install/uninstall helpers, and updated install guidance.

## Source code and build docs

This **Reflect** repository is for releases and user-facing docs. Application source, architecture notes, and build steps live in **[mbaumannn/roomcorrector](https://github.com/mbaumannn/roomcorrector)**:

- [Architecture](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/ARCHITECTURE.md)
- [Execution checklist (TODO)](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/TODO.md)

## Feedback

Report issues via GitHub Issues and include:

- macOS version
- Device/output hardware
- What you expected vs what happened
- Relevant Console logs (filter on `Reflect`)
