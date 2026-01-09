# Reflect — Room Correction for macOS

Reflect is a system-wide room correction app for macOS. It applies parametric EQ filters from Room EQ Wizard (REW) to all audio output.

## Releases

### v1.0.0-beta4 (2026-01-09) ⭐ **Latest**
**Latency Stabilization**

- **Latency Cap**: Implemented target-latency cap to prevent backlog buildup (3-6 buffer periods).
- **Buffer Negotiation**: Driver and app now negotiate and enforce buffer sizes correctly.
- **Visuals**: Added latency estimation to status display.
- **Stability**: Fixed CoreAudio errors during buffer size changes.
- **Notes**:
  - Unsigned beta (Right-click → Open on first launch)
  - Installer handles all setup automatically

📥 **[Download Reflect-Beta-v1.0.0-beta4.dmg](https://github.com/mbaumannn/Reflect/releases/download/v1.0.0-beta4/Reflect-Beta-v1.0.0-beta4.dmg)** | [Release Notes](https://github.com/mbaumannn/Reflect/releases/tag/v1.0.0-beta4)

### v1.0.0-beta3 (2026-01-09)
**Double-Click Installer**

- **✨ New**: One-click installer script — just double-click `Install Reflect.command`
- **✨ New**: Uninstaller script for clean removal
- **🐛 Fixed**: Menu bar icon now white when inactive (was barely visible gray)
- **🎨 Improved**: Orange/amber icon when actively processing
- **📦 Packaging**: Automated driver installation, Gatekeeper bypass, and audio restart
- **Notes**:
  - Unsigned beta (Right-click → Open on first launch)
  - Installer handles all setup automatically

📥 **[Download Reflect-Beta-v1.0.0-beta3.dmg](https://github.com/mbaumannn/Reflect/releases/download/v1.0.0-beta3/Reflect-Beta-v1.0.0-beta3.dmg)** | [Release Notes](https://github.com/mbaumannn/Reflect/releases/tag/v1.0.0-beta3)

### v1.0.0-beta2 (2026-01-09)
**Performance Update**

- **vDSP Optimization**: Rewrote biquad processor to use Accelerate framework SIMD operations.
- **CPU Usage**: Reduced processing CPU from ~8% to <1% when menu closed.
- **UI Polish**: Removed redundant glass material layer for cleaner rendering.
- **Notes**:
  - Unsigned beta (requires Right-Click → Open on first launch).
  - Includes `RoomCorrectorDriver` v1.0 (loopback).

📥 **[Download Reflect-Beta-v1.0.0-beta2.dmg](https://github.com/mbaumannn/Reflect/releases/download/v1.0.0-beta2/Reflect-Beta-v1.0.0-beta2.dmg)**

### v1.0.0-beta1 (2026-01-08)
**First Beta Release**

- **System-Wide Audio Processing**: Applies PEQ corrections to all system audio.
- **REW Import**: Import filter coefficients directly from Room EQ Wizard text exports.
- **Visual Feedback**: Real-time frequency response graph and low-CPU breathing baseline visualization.
- **Performance**: Optimized generic biquad filtering with minimal CPU impact.
- **Notes**:
  - Unsigned beta (requires Right-Click → Open on first launch).
  - Includes `RoomCorrectorDriver` v1.0 (loopback).

📥 **[Download Reflect-Beta-v1.0.0-beta1.dmg](https://github.com/mbaumannn/Reflect/releases/download/v1.0.0-beta1/Reflect-Beta-v1.0.0-beta1.dmg)**

## Installation

Download the DMG and follow the included `INSTALL.md`.

## Requirements

- macOS 13 (Ventura) or later
- Room EQ Wizard filter export (for correction filters)

## Measurements & Filters (REW)

To create the measurements and PEQ filters Reflect uses, see: `REW.md`.

Notes:
- An iPhone mic can be used for a quick start, but a calibrated measurement mic is strongly recommended for best results.
- Start by generating filters for low frequencies (room modes), and prefer cuts over boosts.

## Status

🚧 **Beta** — Currently in private testing. Unsigned builds require manual installation steps.

## Feedback

Report issues in the [Issues](../../issues) tab.
