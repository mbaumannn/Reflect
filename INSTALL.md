# Reflect Beta — Installation Guide

> ⚠️ **Beta Notice**: This is unsigned beta software. macOS will show security warnings during installation. These steps are required until we release a signed version.

## System Requirements

- macOS 13 (Ventura) or later
- Apple Silicon or Intel Mac
- Administrator access

## What's in the DMG

- `Reflect.app` — The menu bar application
- `RoomCorrectorDriver.driver` — Virtual audio device driver
- `INSTALL.md` — This file

## Quick Installation (Recommended)

1. **Right-click** (or Control-click) `Install Reflect.command` and select **Open**.
   > *Note: If you just double-click, macOS may block it with a "Malware" or "Unverified Developer" warning. This is normal for unsigned beta software. Right-click > Open allows you to bypass this.*
2. Click **Open** in the dialog window.
2. Enter your admin password when prompted (terminal window will open).
3. The script will automatically:
   - Install `RoomCorrectorDriver.driver` to `/Library/Audio/Plug-Ins/HAL/`
   - Copy `Reflect.app` to `/Applications/`
   - Restart the audio system (`coreaudiod`)
   - Launch the app

## Manual Installation

If you prefer to install manually or the script fails, follow these steps:

### Step 1: Install the Driver

The driver must be installed to a system directory. This requires your admin password.

**Option A: Using Finder**

1. Open a new Finder window
2. Press `Cmd + Shift + G` (Go to Folder)
3. Type `/Library/Audio/Plug-Ins/HAL/` and press Enter
4. Drag `RoomCorrectorDriver.driver` from the DMG into this folder
5. Enter your admin password when prompted

**Option B: Using Terminal**
```bash
sudo cp -R /Volumes/Reflect\ Beta/RoomCorrectorDriver.driver /Library/Audio/Plug-Ins/HAL/
```

### Step 2: Install the App

Drag `Reflect.app` to your `/Applications/` folder.

### Step 3: Restart the Audio System

The driver won't be recognized until the audio daemon restarts.

Open Terminal and run:
```bash
sudo killall coreaudiod
```

Your audio will briefly stop and resume. This is normal.

### Step 4: Verify Driver Installation

1. Open **Audio MIDI Setup** (search in Spotlight)
2. Look for "RoomCorrector" in the device list
3. It should show both input and output streams

If you don't see it, try restarting your Mac.

### Step 5: First Launch (Bypass Gatekeeper)

Because the app is unsigned, macOS will block it on first launch.

1. In Finder, navigate to `/Applications/`
2. **Right-click** (or Control-click) on `Reflect.app`
3. Select **Open** from the context menu
4. Click **Open** in the security dialog

You only need to do this once. After that, you can launch normally.

### Step 6: Grant Permissions

On first launch, Reflect will request microphone access. This is required to capture audio from the virtual device.

1. Click **OK** when the permission dialog appears
2. If you accidentally denied it, go to:
   - System Settings → Privacy & Security → Microphone
   - Enable the toggle for Reflect

## Using Reflect

1. Click the waveform icon in your menu bar
2. Click **Start Processing**
   - Reflect will automatically set your system output to "RoomCorrector"
3. Select your physical output device (DAC/speakers) from the dropdown
4. Import your REW filters using **Import REW Filters...**
5. Toggle **Bypass** to compare corrected vs uncorrected audio

## Uninstallation

### Quick Uninstall (Recommended)

1. Double-click **`Uninstall Reflect.command`** from the DMG.
2. Enter admin password when prompted.

### Manual Uninstall

#### Remove the App

Drag `Reflect.app` from `/Applications/` to Trash.

### Remove the Driver

**Option A: Using Finder**

1. Press `Cmd + Shift + G` in Finder
2. Go to `/Library/Audio/Plug-Ins/HAL/`
3. Drag `RoomCorrectorDriver.driver` to Trash
4. Enter admin password when prompted

**Option B: Using Terminal**
```bash
sudo rm -rf /Library/Audio/Plug-Ins/HAL/RoomCorrectorDriver.driver
```

### Restart Audio Daemon
```bash
sudo killall coreaudiod
```

## Troubleshooting

### "RoomCorrector" doesn't appear in Audio MIDI Setup

1. Verify the driver is in `/Library/Audio/Plug-Ins/HAL/`
2. Run `sudo killall coreaudiod`
3. If still missing, restart your Mac

### No audio output after starting Reflect

1. Check that a physical output device is selected in the Reflect dropdown
2. Verify the physical device is connected and working
3. Check System Settings → Sound → Output shows "RoomCorrector"

### App shows "Microphone permission required"

1. Go to System Settings → Privacy & Security → Microphone
2. Find Reflect in the list and enable it
3. If Reflect isn't listed, try launching it again

### Audio dropouts or crackling

1. Open Reflect settings
2. Increase buffer size (trade latency for stability)
3. Close CPU-intensive applications

### App won't open ("Apple cannot check for malicious software")

1. Right-click the app and select **Open** (not double-click)
2. If that fails:
   - System Settings → Privacy & Security
   - Find the "Reflect was blocked" message
   - Click **Open Anyway**

## Providing Feedback

Please report issues at: https://github.com/mbaumannn/Reflect/issues

Include:
- macOS version
- Mac model (Intel/Apple Silicon)
- Steps to reproduce the issue
- Console logs if relevant (`Console.app` → filter by "Reflect" or "RoomCorrector")

## Known Limitations (Beta)

- Unsigned: requires manual Gatekeeper bypass
- Manual driver installation required
- No automatic updates
- [Add other known issues here]
