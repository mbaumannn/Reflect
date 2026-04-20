# Reflect Installation Guide

Version: **v0.10.1**

> Reflect is unsigned. macOS will block the app and helper scripts on first use until you approve them in **Privacy & Security**.

## System Requirements

- macOS 14.2 or later
- Apple Silicon or Intel Mac

## DMG Contents

- `Reflect.app`
- `Applications` (symlink — drag target)
- `Install Reflect.command`
- `Uninstall Reflect.command`
- `INSTALL.md`
- `REW.md`

## Install in 3 Steps

1. Mount `Reflect-*.dmg`.
2. Drag `Reflect.app` onto the **Applications** folder in the DMG window.
3. Follow the **macOS Security** steps below, then launch Reflect and grant Audio Capture permission when prompted.

Then load filters in **Correct** mode, or use **Measure** and **Apply Filters**, choose your output device in Reflect, and press **Start Processing**.

## macOS Security (Unsigned Build)

Because Reflect is not signed with an Apple Developer certificate, macOS blocks the app and helper scripts on first use. This is expected.

### Opening Reflect.app

When you double-click Reflect for the first time, macOS shows:

> **"Reflect" cannot be opened because Apple cannot check it for malicious software.**

Steps:

1. Open **System Settings → Privacy & Security**.
2. Scroll down to the **Security** section.
3. You will see: *"Reflect was blocked from use because it is not from an identified developer."*
4. Click **Open Anyway**.
5. Confirm **Open** in the dialog that appears.

Reflect will open normally after this one-time approval.

**Terminal shortcut** — does the same thing in one command:
```bash
xattr -dr com.apple.quarantine /Applications/Reflect.app
```

### Running Install Reflect.command or Uninstall Reflect.command

The `.command` scripts are also blocked on first run. To open them:

- Right-click the script → **Open** → click **Open** in the confirmation dialog.

If that doesn't work, run from Terminal:
```bash
bash "/Volumes/Reflect/Install Reflect.command"
```

## Permission Recovery

If Audio Capture permission was denied:

1. Open **System Settings → Privacy & Security → Audio Capture**
2. Enable Reflect
3. Return to Reflect and press **Start Processing** again

## Uninstall

1. Run `Uninstall Reflect.command` (right-click → Open first), or remove `Reflect.app` from `/Applications` manually.
2. Optionally remove preferences when prompted.

## Troubleshooting

### No audio after pressing Start

- Confirm a real output device is selected in Reflect.
- Press Stop, then Start once.
- If the selected device disappeared, select it again in Reflect.

### Permission Required shown in app

- Grant Audio Capture permission in System Settings → Privacy & Security.
- Return to app and retry Start Processing.

### Device switch issues

- Reflect uses the output device selected inside Reflect.
- If you change the macOS output device, confirm the same device is selected in Reflect.
- Reflect 0.10.1 improves live recovery when macOS output changes repeatedly.
- If audio still does not recover after extreme device switching, stop processing once, confirm the intended output is selected in Reflect, then start again.

## Migration / Rollback

If you are migrating from the old driver-based setup, see:

- [Migration and rollback (roomcorrector)](https://github.com/mbaumannn/roomcorrector/blob/main/Docs/MIGRATION.md)

Rollback to v1 requires using an earlier source revision; the current release line is app-only.
