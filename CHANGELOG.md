# Changelog

*[Version française → CHANGELOG.fr.md](CHANGELOG.fr.md)*

All notable changes to X5 Studio are listed here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow [Semantic Versioning](https://semver.org/).

## [1.8.2] — 2026-11-22

### Added
- Two screenshots in `docs/screenshots/` (Quick tab and Filter tab), shown in README.md (English) and LISEZMOI.md (French).

### Fixed
- The SysEx monitor showed long messages as "(194 o)", a French unit left in the English interface. It now reads "194 bytes", translated in every language.

## [1.8.1] — 2026-11-22

### Fixed
- **Vary** made changes too small to hear: with the default amount, the filter cutoff moved by about 3 steps out of 99. The **Amount** slider now means the largest change in % of each parameter's range (±12 % by default, up to ±40 %, shown next to the slider), and the cutoff weighs a little more.
- Values at a limit (a level at 99, a colour at 0) no longer get stuck: they bounce back, so every draw really changes each ticked parameter.
- The **Tone** box no longer changes "Colour ← velocity", which is only heard when playing harder or softer.

### Added
- A summary line under the Vary buttons lists what moved, biggest changes first (for example "Cutoff 70→81 · Colour 0→9").

## [1.8] — 2026-11-22

### Added
- **Inspiration** (Quick tab, both views): pick a family (Pad, Bass, Lead, Keys, Bell, Percussive, Texture / FX or Surprise) and a new sound is created from scratch. Each family has its own rules (multisound families, envelope shapes, filter, vibrato, Single or Double mode, suitable effects), so results stay playable. **Another one** repeats the same family; **Previous sound** goes back (one undo step).
- New sounds get a **short name** (10 characters, the X5's limit) built from word lists in the interface language. Word lists live in the language files (`names`), with adjective-after-noun order for French, Italian and Spanish.
- **Code documentation:** an overview at the top of the script ("How this program works": the central 164-byte buffer, how a change travels to the X5, map of the sections) and an explanation of the role of each section. All code comments are now in English.

### Fixed
- The name display cut off the 10th character.

## [1.7.1] — 2026-11-22

### Changed
- **Test keyboard in a floating window**, opened with the **🎹** button in the header, movable by its title bar and resizable. It is closed by default and its state is remembered. The computer keys still play notes when it is closed. The SysEx monitor and the log now sit at the bottom of the screen and move up when the keyboard is open.
- **Single theme (Atelier).** The dark **Nuit** theme and its ☾ / ☀ button are disabled; the theme is kept as a comment in the code so it can be brought back.

## [1.7] — 2026-11-22

### Added
- **X5 page numbers on the cards** (for example `4A–4E`), matching the X5's own Program edit pages (PROG → EDIT). They follow the oscillator mode (Single/Drums or Double) and the oscillator being edited; with both oscillators linked, both page ranges are shown.

### Changed
- **Effects:** placement (page 20A in Double mode) and the dry/effect balances of both effects (page 20B) are now together in a single **Routing & balance** card, visible in both views.
- The effects' Sine/Triangle setting is now labelled **Wave Shape**, as on the X5's screen.

## [1.6] — 2026-11-22

### Added
- **Detailed effect editor** (Effects tab, Full view): every setting of each of the 47 effect types, following the "Effect Parameter" tables of the Korg manual. Reverb time is shown in seconds, LFO speeds in Hz, delays in ms and EQ in dB.
- For each effect: **On/Off** switch, **wet/dry balance** L and R (linked by default), and **dynamic modulation** (source: joystick, aftertouch, pedals, VDA EG; amount −15…+15).
- Choosing an effect type now loads starting values for that type and switches the effect on.

### Changed
- Effect settings, including type changes, are sent to the X5 as a whole sound (Program Dump), at most every 150 ms while a control moves. The order of the X5's effect Parameter Change messages does not follow the manual, so the dump route is the reliable one.
- Effects tab layout: routing on top, the two effects side by side.

### Fixed
- Undo/redo of an effect On/Off change was not sent to the X5.

## [1.5.2] — 2026-11-22

### Changed
- **Same tabs in both views.** The Controllers tab is gone: its Aftertouch and Joystick settings now sit at the bottom of the **Modulation** tab (formerly "Pitch & LFO"), in Full view only.

## [1.5.1] — 2026-11-22

### Changed
- **English is now the interface's base language**, written directly in `x5studio.html`.
- **French, Italian, Spanish and German moved to a `lang/` folder**, one file per language (`lang/fr.js`, `it.js`, `es.js`, `de.js`). Each file holds the interface texts and the "?" help. Fixing or adding a language no longer means touching the application code.
- The first-launch language still follows the browser, and the last choice is still remembered.
- If the `lang/` folder is missing, the app keeps working in English and says so in the log.

No change in features or MIDI behaviour.

## [1.5] — 2026-11-22

### Added
- **Essential / Full** switch, left of the tabs, remembered between sessions. **Essential** (default) keeps the main settings: multisounds, filter and amp envelopes, cutoff, colour, velocity depth, vibrato, filter LFO, effect types. **Full** shows every Program parameter, as before. Both views edit the same sound; switching never sends anything to the X5.
- In Essential view, these are hidden: the Controllers tab, the detailed EG time/level sliders (the envelope editors remain), keyboard tracking, the −/0/+ sensitivity switches, Pitch EG, pan and C/D sends, osc 2 delay, Hold, and LFO sync/key tracking.

## [1.4] — 2026-11-21

First public release on GitHub.

### Added
- **● Editing / ○ Play** button in the header. It shows whether the X5 is in edit mode, and one click hands control back to the synth with a Mode Change to Program (`F0 42 3n 36 4E 02 00 F7`).
- The X5 is put back in Program (play) mode automatically when the page is closed or reloaded.
- **Re-entering edit mode:** after leaving it, the next change sends a Mode Change to Prog Edit, waits 100 ms, then resends the whole sound, so the synth and the editor stay identical.
- **Recovery after a rejected change (NAK):** the app puts the X5 back in edit mode and resends the sound, and ignores the repeated NAKs the synth often sends.
- The app follows mode changes made on the X5's front panel. **Detect** also asks the synth for its current mode (Mode Request).
- The SysEx monitor decodes Mode Change, Mode Request and Mode Data messages.

## [1.3] — 2026-11-21

### Added
- **Atelier** theme (light, inspired by the look of Eurorack modules): module-style cards with screws, white knobs, and one colour per section (oscillators, filter, amp, pitch & LFO, effects).
- **Nuit** theme (the previous dark look), switched with the ☾ / ☀ button and remembered.

### Fixed
- **Pitch EG:** "Levels ← velocity" and "Times ← velocity" were swapped.
- **Send bus C / D** were swapped.
- **Drums mode:** drum kit numbers are now correct (0–1 = user kits, 8–15 = ROM kits 1–8).
- Envelope shading could disappear on some pages.

These fixes come from the official X5DR MIDI implementation tables transcribed in Mark Baylis's [x5dr-editor](https://github.com/Baylo1/x5dr-editor).

## [1.2] — 2026-11-21

### Added
- Interface in **French, English, Italian, Spanish and German**, with a flag selector. On first launch, the app uses the browser's language.
- Help translated into the five languages.

### Changed
- Released under the **MIT License**.

## [1.1] — 2026-11-21

### Added
- **SysEx monitor:** a movable, resizable window showing every message sent and received, decoded in plain words, with copy, pause and a filter for notes.
- **Send delay:** an adjustable pause after each SysEx message (0–150 ms, 20 ms by default). Messages are queued in order, taking real MIDI transmission time into account.
- Clearer messages when the browser blocks MIDI access, with a retry button.
- Copyright notice.

## [1.0] — 2026-11-21

### Added
- Single-file Web MIDI editor for Korg **X5 / X5D / X5DR / 05R/W** Programs (Chrome / Edge).
- All Program parameters: oscillators (340 multisounds, searchable by family), VDF, VDA, Pitch EG, LFOs, aftertouch and joystick, plus effect types and routing.
- Draggable envelopes, 10 macros, **Vary** (random variations), undo/redo, **A/B** compare.
- Live editing (Parameter Change) or manual send (Program Dump), read from the X5, write to a memory slot.
- On-screen and computer keyboard, test phrases, auto-replay after each change.
- Library: read or send a 100-sound bank, open and save `.syx` files, keep sounds in the browser.

### Fixed (compared with the Ctrlr 05R/W panel it is based on)
- Negative values were sent as invalid MIDI bytes.
- Velocity and keyboard sensitivity switches now have their three states (−/0/+).
- Keyboard tracking has its four modes (Off/Low/High/All).

[1.8.2]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.8.2
[1.8.1]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.8.1
[1.8]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.8
[1.7.1]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.7.1
[1.7]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.7
[1.6]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.6
[1.5.2]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5.2
[1.5.1]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5.1
[1.5]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.5
[1.4]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.4
