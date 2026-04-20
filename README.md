# Reflect - Room Correction for macOS

Reflect is a system-wide room correction app for macOS using driverless CoreAudio Process Taps.

## Status

Reflect v2 is in beta. Build is unsigned — first launch requires a Gatekeeper override (right-click → Open).
Current release: **v0.10.1**

## Requirements

- macOS 14.2 or later
- Apple Silicon or Intel Mac
- REW filter export text file (optional, for EQ correction without measuring)

## Quick Install

1. Download and mount the latest Reflect DMG.
2. Drag `Reflect.app` to the **Applications** folder in the DMG window.
3. **macOS will block the app on first launch** (unsigned build). Go to **System Settings → Privacy & Security → scroll down → Open Anyway** → confirm Open. This is a one-time step.
4. Grant Audio Capture permission when prompted. Load filters (**Correct** mode: import icon → REW Generic text, or **Measure** mode: complete a run and **Apply Filters**), pick your output, then press **Start Processing**. Use the **Correction Strength** slider to tune intensity.

Full install guide including Gatekeeper steps and troubleshooting: [INSTALL.md](INSTALL.md)

Detailed steps: [INSTALL.md](INSTALL.md)

## Measuring with REW / Importing Filters

Reflect includes a built-in **Measure** mode for automatic room correction — no external software needed. If you prefer to measure in Room EQ Wizard and import the resulting filters manually, see [Measuring with REW and Importing Filters](REW.md).

## Migration and Rollback

If you previously used the legacy driver build, use the migration guide in the **roomcorrector** source repository:

- [Migration and rollback](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/MIGRATION.md)

## Known Limitations

- Unsigned build — first-launch Gatekeeper override required (right-click → Open).
- No automatic updates.
- No per-app routing.
- No IR convolution in the v2 runtime.

## What's New in v0.10.1

### Reliability

- Fixed repeated output-device switching in macOS sound settings so Reflect now rebinds processing cleanly without falling into an error state after several successful recoveries
- Improved hot-switch handling when external interfaces are connected, re-enumerated, or selected repeatedly while processing is active
- Restored in-app FAQ/help links so measurement guidance remains reachable from the updated UI

## What's New in v0.10.0

### Measurement pipeline — complete rewrite

Reflect's Auto-EQ pipeline was rebuilt from scratch and validated against professional room correction references across two independent real-room datasets:

- **>97% filter accuracy** on both test rooms (98.66% / 97.35%)
- **Self-contained target estimation** — Reflect computes the correction reference from its own measurement trace using a full-range log-weighted energy mean; no external metadata required
- **Prominence-based peak detection** with 3 dB threshold and 15 Hz minimum spacing — finds the peaks that actually matter in the 20–200 Hz range
- **Joint frequency + Q refinement** — every filter's center frequency and bandwidth are jointly optimised after placement, not just the gain
- **Hump stabilization** — detects and resolves redundant overlapping peaks in the 170–220 Hz range that commonly appear in real rooms, then backfills with the next-best candidate if it improves the fit
- Validated by a per-filter test suite with ±1 dB gain and ±1.0 Q tolerances against canonical benchmark fixtures from two separate rooms
- Measurement sweeps now route through the selected output device

### UI redesign

- Five-state linear processing flow: Idle → Measuring → Review → Applying → Active
- Studio Amber accent color throughout; new dark navy + orange activity wave icon
- Unified **SettingsPanel** with About, Settings, and FAQ tabs (replaces scattered sheets)
- **Correction Strength** slider — scale filter intensity without re-importing
- Export active filters back to REW Generic text directly from Correct mode

### Graph and analysis

- Response curves centred at 0 dB reference line
- Frequency-windowed X axis with clipping fixes; dynamic ±24 dB Y scale
- Predicted curve uses calibrated response; auto-refits when target changes

### FAQ and onboarding

- Card layout with SF Symbol icons; gradient scroll affordance
- iPhone-as-measurement-mic guidance added
- Send Feedback button in About tab

## Source code and build docs

This **Reflect** repository is for releases and user-facing docs. Application source, architecture notes, and build steps live in **[mbaumannn/roomcorrector](https://github.com/mbaumannn/roomcorrector)**:

- [Architecture](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/ARCHITECTURE.md)
- [Measurement pipeline PRD](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/PRD-python-experiments-into-Reflect.md)

## Feedback

Report issues via GitHub Issues and include:

- macOS version
- Device/output hardware
- What you expected vs what happened
- Relevant Console logs (filter on `Reflect`)
