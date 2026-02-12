# REW Measurements (Room EQ Wizard)

Reflect uses **parametric EQ (PEQ)** filters exported from **Room EQ Wizard (REW)**. This guide is a generally applicable walkthrough: from downloading REW, to making room measurements, to generating PEQ filters you can import into Reflect.

Reflect v2 is driverless/app-only, so you do not need to install any virtual audio driver before using this workflow.

## What You Need

- A Mac (or Windows/Linux) running REW
- Your normal playback chain (DAC/audio interface → amplifier/monitors/headphones)
- A microphone for measurement:
  - **Recommended**: a calibrated measurement mic (e.g. miniDSP UMIK‑1, Dayton UMM‑6, or any mic with a calibration file)
  - **Possible (quick start)**: an iPhone as a mic can work for rough measurements, but expect reduced accuracy (especially in bass and treble) and device/OS limitations

## 1) Download + Install REW

1. Download REW from `https://www.roomeqwizard.com/`.
2. Install and launch REW.
3. If you have a measurement mic calibration file (often a `.txt`), keep it handy.

## 2) Prepare Your System (Important)

To get consistent measurements, you want a clean signal path.

- Set a fixed sample rate for your playback device (commonly **48 kHz**):
  - macOS: **Audio MIDI Setup** → select your output device → set **Format** to `48000.0 Hz`
- Disable extra processing:
  - Turn off any system‑wide EQ, “sound enhancements”, app EQ, DAW plugins, or monitor DSP
  - Disable system sounds/notifications during measurement
- Keep your speaker placement and listening setup unchanged while capturing a set of measurements.

## 3) Connect and Select Devices in REW

Open **REW → Preferences → Soundcard**:

- **Output device**: your DAC/audio interface (the device that feeds your speakers/headphones)
- **Output channels**: typically `1+2` (stereo)
- **Input device**:
  - Measurement mic (USB mic or interface input), or
  - iPhone mic *only if it appears as a selectable audio input device on your system*
- **Input channel**: mono (one mic channel)
- **Sample rate**: match your OS setting (e.g. **48 kHz**)

### Microphone calibration (recommended)

If you have a mic calibration file:

- **REW → Preferences → Mic/Meter** → load the cal file

If you’re using an iPhone mic (or any uncalibrated mic), you can still measure and improve obvious room issues, but avoid making strong decisions from the extreme lows/highs and treat results as approximate.

## 4) Mic Placement (The Part That Matters Most)

For a typical listening position measurement:

- Put the mic at **ear height**, at the listening position
- Point the mic **straight up** (common practice for omni measurement mics and phones)
- Use a **stand/tripod**; don’t hold the mic by hand
- Keep the mic position **identical** across L/R/L+R sweeps

If you care about an “area” (not a head‑in‑a‑vise point), measure a few positions around your listening spot (small movements of 10–30 cm) and average.

## 5) Multiple Mic Positions + Proper Averages

Single-point measurements can change a lot with tiny mic movements. If you want EQ that stays helpful when you shift in your chair, use multiple mic positions and average them.

### Recommended approach (a small “listening bubble”)

Pick 3–9 mic positions around your main listening spot:

- Center (your exact head position)
- Slightly forward/back/left/right (10–30 cm)
- Keep **ear height** and **mic pointing up** for every position

Keep everything else identical:

- Same REW settings, sweep level, and output gain
- Same speaker placement and volume
- Same room conditions (doors closed, HVAC noise minimized)

### What to average (depends on how you’ll apply EQ)

- **Per-channel EQ (best if your app supports L/R separately)**:
  - Measure **Left-only** at each mic position → average those Left traces → generate Left filters
  - Measure **Right-only** at each mic position → average those Right traces → generate Right filters
  - Use **L+R** measurements as a sanity/validation check (not as the design trace)
- **One shared EQ (same filters applied to both channels)**:
  - Measure **L+R** at each mic position → average those L+R traces → generate one filter set

Avoid averaging Left-only and Right-only together into one “summed” trace if you’re going to apply different filters per channel—designing per channel from per-channel averages is more robust.

### How to make an average in REW

1. Run and name your measurements clearly, e.g.:
   - `Nearfield A - L`, `Nearfield B - L`, `Nearfield C - L`
2. Open **All SPL**.
3. Tick the traces you want to average (only the set that should be averaged together).
4. Use REW’s **Average the Responses** function to create a new averaged trace.
5. Rename the averaged trace to something obvious, e.g. `Nearfield Avg - L`.

Use the averaged trace as the “design” trace for generating EQ filters.

## 6) Run Measurements (L, R, L+R)

Click **Measure** to open the measurement dialog.

Suggested starting settings:

- **Sweep range**: `20 Hz – 20 kHz`
- **Sweep level**: start around `-20 dBFS` and adjust after “Check Levels”

### Level check (avoid clipping)

1. In the measurement dialog, click **Check Levels**.
2. Increase output level using your interface/monitor volume (not random OS sliders).
3. Aim for a strong signal without clipping; leave headroom (peaks well below 0 dBFS).

### Measurement set (single position)

At one mic position, do three sweeps:

1. **Left only** (mute/right speaker off)
2. **Right only** (mute/left speaker off)
3. **Both** (L+R)

Name each measurement clearly, for example:

- `Nearfield - L`
- `Nearfield - R`
- `Nearfield - L+R`

### Two (or more) positions

Repeat the same L/R/L+R set at a second location you care about (e.g. “behind desk”), then compare:

- L vs R (speaker/room asymmetry)
- Nearfield vs behind desk (how much the room changes with position)

## 7) Sanity Check the Results

Before generating filters:

- Confirm no sweep clipped (re‑measure at a lower level if it did)
- Use light smoothing (e.g. **1/12 octave**) to see broad trends without hiding big problems
- Focus EQ efforts on **low frequencies** first; above a few hundred Hz you’ll mostly see position‑dependent comb filtering that EQ can’t “fix” reliably

## 8) Generate PEQ Filters in REW (for Reflect)

### Pick a “design” trace

Choose the measurement that matches how you’ll apply correction:

- **Per‑speaker correction**: generate filters from `L` and `R` separately
- **Single shared correction**: generate filters from an `L+R` measurement or an **average** of several nearby mic positions

### Create conservative, robust filters

1. Select your measurement trace.
2. Open the **EQ** window.
3. Set **Equaliser** to `Generic`.
4. In **Target Settings**:
   - Click **Calculate target level from response** (this sets the “base” / **target level** so REW isn’t trying to apply lots of boost just to reach the target)
   - Prefer **cuts over boosts** (deep nulls are usually not fixable with boost)
5. In **Match Range**:
   - Start with something like `20 Hz – 200 Hz` (typical range where PEQ helps most with room modes)
6. Generate filters with **Match response to target**.

Practical tips:

- If REW proposes extreme, very narrow cuts (very high Q), try disabling **Allow narrow filters below 200 Hz** or manually reduce the depth/Q for a more position‑robust result.
- Keep the number of filters reasonable; fewer filters that reliably help is better than many filters that overfit one mic position.

### Export from REW

In the EQ window, export as a text “Filter Settings” file (the format that starts with `Room EQ V5...` and lists filters like `Filter 1: ON PK Fc ...`).

Then import that file into Reflect via **Import REW Filters…**.

## Troubleshooting

- **My iPhone doesn’t show up as an input device in REW**: that’s common. The simplest path is using a USB measurement mic. If you do use a phone, you may need a separate workflow/app to present the phone audio as a standard input device to the computer.
- **The response looks wildly different between runs**: check mic placement (movement of a few cm matters), disable any hidden DSP/EQ, and ensure sample rates match between OS and REW.
- **REW warns the response is “below target”**: lower the target level (use **Calculate target level from response**) and avoid boost-heavy targets by setting max boost limits and focusing on peak cuts.
