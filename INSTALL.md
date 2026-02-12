# Reflect Installation Guide (v2 App-only)

Version: **v1.0.0-beta5**

> Beta notice: Reflect pre-release builds are currently unsigned.

## System Requirements

- macOS 14.2 or later
- Apple Silicon or Intel Mac

## DMG Contents

- `Reflect.app`
- `Install Reflect.command`
- `Uninstall Reflect.command`
- `INSTALL.md`
- `REW.md`

## Install in 3 Steps

1. Mount `Reflect-*.dmg`.
2. Install the app:
   - Recommended for testers: run `Install Reflect.command` (copies app + removes quarantine), or
   - Drag `Reflect.app` to `/Applications`.
3. Launch Reflect and grant Audio Capture permission when prompted.

Then select your output device and press **Start Processing**.

## First Launch (Unsigned Build)

If macOS blocks launch:

1. Open Finder -> `/Applications`
2. Right-click `Reflect.app` -> **Open**
3. Confirm **Open** in the dialog

Optional terminal fallback:

```bash
xattr -dr com.apple.quarantine /Applications/Reflect.app
```

## Permission Recovery

If permission was denied:

1. In Reflect, click **Open Settings**, or open:
   - System Settings -> Privacy & Security -> Audio Capture
2. Enable Reflect
3. Return to Reflect; start processing again

## Uninstall

1. Run `Uninstall Reflect.command`, or remove `Reflect.app` manually.
2. Optionally remove preferences when prompted.

## Troubleshooting

### No audio after pressing Start

- Confirm a real output device is selected in Reflect.
- Press Stop, then Start once.
- Re-open Reflect after device/samplerate changes.

### Permission Required shown in app

- Grant Audio Capture permission in System Settings.
- Return to app and retry Start Processing.

### Device switch issues

- Stop processing.
- Reconnect/select target output.
- Start processing again.

## Migration / Rollback

If you are migrating from the old driver-based setup, see:

- [roomcorrector migration guide](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/MIGRATION.md)

Rollback to v1 requires using an earlier source revision; v2 runtime is now the active path.
