# Reflect — Room Correction for macOS

Reflect is a system-wide room correction app for macOS. It applies parametric EQ filters from Room EQ Wizard (REW) to all audio output.

## Releases

### v1.0.0-beta1 (2026-01-08)
**First Beta Release**

- **System-Wide Audio Processing**: Applies PEQ corrections to all system audio.
- **REW Import**: Import filter coefficients directly from Room EQ Wizard text exports.
- **Visual Feedback**: Real-time frequency response graph and low-CPU breathing baseline visualization.
- **Performance**: Optimized generic biquad filtering with minimal CPU impact.
- **Notes**:
  - Unsigned beta (requires Right-Click → Open on first launch).
  - Includes `RoomCorrectorDriver` v1.0 (loopback).

📥 **[Download Reflect-Beta-v1.0.0-beta1.dmg](./releases/Reflect-Beta-v1.0.0-beta1.dmg)**

## Installation

Download the DMG and follow the included `INSTALL.md`.

## Requirements

- macOS 13 (Ventura) or later
- Room EQ Wizard filter export (for correction filters)

## Status

🚧 **Beta** — Currently in private testing. Unsigned builds require manual installation steps.

## Feedback

Report issues in the [Issues](../../issues) tab.
