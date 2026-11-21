# Changelog

*[Version française → CHANGELOG.fr.md](CHANGELOG.fr.md)*

All notable changes to X5 Studio are listed here. The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow [Semantic Versioning](https://semver.org/).

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

[1.4]: https://github.com/BenjaminPaty54/x5-studio/releases/tag/v1.4
