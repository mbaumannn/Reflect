# Measuring with REW and Importing Filters

## Two ways to get filters into Reflect

**Option A — Built-in Measure mode (no REW needed)**
Reflect has a native measurement workflow: open the app, switch to **Measure** mode, place your mic, and follow the on-screen prompts. Reflect captures the sweep, analyses the room response, and generates parametric EQ filters automatically. Hit **Apply Filters** to load them into **Correct** mode. No external software required.

**Option B — Measure in REW, import into Reflect (this guide)**
If you want full control over the measurement process, want to use REW's averaging or windowing tools, or prefer to inspect and manually tune the EQ curve before importing — use REW to measure and generate filters, export them as a text file, and import that file into Reflect's **Correct** mode. This guide covers that workflow end-to-end.

---

Reflect v2 is driverless/app-only — you do not need to install any virtual audio driver before using either workflow.

Reflect currently applies one shared filter set to the selected stereo output. When preparing filters in REW, design a single correction set for your listening position rather than separate left/right imports.

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

## 5) Multiple Mic Positions + Averages

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

### What to average for Reflect

- Reflect uses one shared filter set for stereo playback.
- For the final design trace, use an **L+R** measurement or an average of several nearby **L+R** measurements.
- You can still measure **Left** and **Right** separately in REW to diagnose speaker or room asymmetry, but those are best used for analysis, not as separate imports into Reflect.

### How to make an average in REW

1. Run and name your measurements clearly, e.g.:
   - `Nearfield A - L+R`, `Nearfield B - L+R`, `Nearfield C - L+R`
2. Open **All SPL**.
3. Tick the traces you want to average (only the set that should be averaged together).
4. Use REW’s **Average the Responses** function to create a new averaged trace.
 5. Rename the averaged trace to something obvious, e.g. `Nearfield Avg - L+R`.

Use the averaged trace as the “design” trace for generating EQ filters.

## 6) Run Measurements

Click **Measure** to open the measurement dialog.

Suggested starting settings:

- **Sweep range**: `20 Hz – 20 kHz`
- **Sweep level**: start around `-20 dBFS` and adjust after “Check Levels”

### Level check (avoid clipping)

1. In the measurement dialog, click **Check Levels**.
2. Increase output level using your interface/monitor volume (not random OS sliders).
3. Aim for a strong signal without clipping; leave headroom (peaks well below 0 dBFS).

### Measurement set (single position)

For the filter set you plan to import into Reflect, the key measurement is **L+R** at the listening position.

Recommended sweep set:

1. **Both** (L+R) for the actual correction trace
2. **Left only** (optional, for diagnosis)
3. **Right only** (optional, for diagnosis)

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

## 8) Generate PEQ Filters in REW for Reflect

### Pick a “design” trace

Choose one shared design trace:

- an `L+R` measurement at the listening position, or
- an average of several nearby `L+R` measurements

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

In the EQ window, click **Export filter settings to text file** (or similar — exact wording varies by REW version). Save as a `.txt` file. The format starts with `Room EQ V5` and lists entries like `Filter 1: ON PK Fc 80 Hz Gain -6.0 dB BW Oct 0.333`.

### Import into Reflect

1. Click the Reflect icon in the menu bar to open the app.
2. Make sure you are in **Correct** mode (top of the popover).
3. Click the **import icon** (↑ arrow) in the bottom footer of the popover.
4. The file picker opens with the prompt **Import REW Filters** — select your exported `.txt` file.
5. Reflect loads the filters and shows them in the PEQ graph. The header displays the source file name.

**After importing:**
- Use the **Correction Strength** slider to scale how aggressively the filters are applied (100% = full filter gain, lower = gentler correction).
- Select your output device and press **Start Processing** to hear the correction live.
- Use the **Bypass** toggle in the footer to A/B between corrected and uncorrected sound.
- To save a backup copy of the loaded filters, click the **export icon** (↓ arrow) in the footer — this exports the current filter set as a new REW Generic text file.

## Troubleshooting

- **My iPhone doesn’t show up as an input device in REW**: that’s common. The simplest path is using a USB measurement mic. If you do use a phone, you may need a separate workflow/app to present the phone audio as a standard input device to the computer.
- **The response looks wildly different between runs**: check mic placement (movement of a few cm matters), disable any hidden DSP/EQ, and ensure sample rates match between OS and REW.
- **REW warns the response is “below target”**: lower the target level (use **Calculate target level from response**) and avoid boost-heavy targets by setting max boost limits and focusing on peak cuts.
