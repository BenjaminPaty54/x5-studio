# X5 Studio

*[Version française → LISEZMOI.md](LISEZMOI.md)*

A sound editor for the **Korg X5, X5D, X5DR and 05R/W** that runs right in your browser (Chrome or Edge) using Web MIDI. Create or tweak a Program (a sound, or "patch") and hear it on the synth instantly, without the old 1990s editing software.

The app is one HTML file, `x5studio.html`, plus a `lang/` folder holding the translations. Nothing to install, and no Internet connection needed. Keep the `lang/` folder next to `x5studio.html`: without it, the app still works, but in English only.

The interface is available in **English, French, Italian, Spanish and German**: click a flag at the top right. On first launch, the app uses your browser's language. English is built into the page; the other languages come from the `lang/` folder (see [Translations](#translations)).

Two views: **Essential** (the main settings, for building or tweaking a sound quickly) and **Full** (every Program parameter), switched left of the tabs.

Two themes: **Atelier** (light, inspired by the look of Eurorack modules) and **Nuit** (dark), switched with the ☾ / ☀ button.

© 2026 Benjamin PATY (BenjaminPaty54)

---

## Requirements

- A Korg X5, X5D, X5DR or 05R/W (they share the same engine and SysEx format).
- A MIDI interface connected to your computer, wired both ways:
  - synth MIDI OUT → interface MIDI IN;
  - interface MIDI OUT → synth MIDI IN.
- **Google Chrome** or **Microsoft Edge** (Safari doesn't support MIDI in web pages).
- Python 3 to run a tiny local server. It's already installed on most Macs.

## Synth settings

1. **GLOBAL → MIDI Filter → EX = ENA**: required, otherwise no SysEx gets through.
2. **Memory Protect Program = OFF**: only if you want to write sounds to memory.
3. Note the **global MIDI channel**. The app can also find it on its own.

## Launching the app

The page has to open in its own tab, served by a small local server. When it's opened from a file preview, or sometimes by just double-clicking it, the browser blocks MIDI access.

```
cd folder/containing/x5studio.html
python3 -m http.server 8000
```

Then open **http://localhost:8000/x5studio.html** in Chrome and allow access to MIDI devices. Keep the terminal open while you use the app.

## Getting started

1. At the top of the page, pick your interface's MIDI **output** and **input**, then click **Detect**: the app finds the synth and its channel automatically.
2. Put the synth in **PROG** mode on the sound you want to edit, then click **⇩ Read X5**.
3. Edit the sound. In **Direct** mode, every change goes to the synth right away.
4. To keep the result, pick a slot (A00 to A99) and click **Write**.

> ⚠️ Back up your sounds before experimenting: **Library** tab → **⇩ Read X5 bank** → **Download bank .syx**.

## The interface

| Tab | What it's for |
|---|---|
| **Quick** | Ten macros (Brightness, Attack, Release, Vibrato, Width…) that each move several parameters at once. Each gesture adds to or subtracts from the current sound, then the macro springs back to the centre. **Vary** suggests small random variations. |
| **Oscillators** | Single / Double / Drums mode, a choice of 340 multisounds (search, families, random pick), octave, level, pan, sends. |
| **Filter (VDF)** and **Amp (VDA)** | Envelopes you edit with the mouse, velocity and keyboard sensitivity. You can edit oscillator 1, oscillator 2, or both at once ("linked"). |
| **Pitch & LFO** | Pitch EG, filter LFO, vibrato. |
| **Controllers** | Aftertouch and joystick. |
| **Effects** | Choice of the two effects and how they're routed. |
| **Library** | Read or send a bank of 100 sounds, open and save `.syx` files, keep favourite sounds in the browser. |

Always-visible tools:

- **Keyboard** on screen or on your computer keyboard (middle row = white keys), **▶ Test** to play a note, a chord or an arpeggio, and **Replay after each change**.
- **↶ / ↷** to undo or redo (Ctrl/⌘+Z), **A/B** (hold it down to hear the original sound), and **Revert to original**.
- **● Editing / ○ Play**: shows whether the X5 is in edit mode. One click hands control back to the synth (Program mode); this also happens automatically when you close the page. If the X5 rejects a change (for example after you used its front panel), the app puts it back in edit mode and resends the sound.
- **SysEx**: a small window that shows every message sent ↑ or received ↓, decoded in plain words with its bytes. The **Delay** slider adds a pause after each SysEx message (20 ms by default).
- Double-click a slider to restore its original value; use the mouse wheel for fine adjustment.

## Current limitations

- **Programs only.** The app edits individual sounds (Programs). It does not create or edit **Combinations** (Combis), which layer or split several Programs from the banks into richer setups. A Combi that uses an edited Program will benefit from the changes, but the Combi itself still has to be edited on the synth.
- **Global settings, Multi mode and the X5DR's GM bank**: not supported.
- **Effects**: you can choose the type of both effects and their routing, but not their internal settings (reverb time, delay time…). Those settings are kept as they are and travel with the sound.
- **Drum kits**: you can pick a kit in Drums mode, but you can't edit what's inside it.
- **Writing to memory**: with no official documentation available, the format of the write command was inferred. The app shows the synth's reply; also check the synth's display to confirm the sound was written.
- **Reading the bank**: on some units you need to start the transfer from the synth (GLOBAL → MIDI Data Dump).
- **Browsers**: Chrome and Edge only.

## Troubleshooting

| Message or symptom | Fix |
|---|---|
| "Midi has been disabled in this document by permissions policy" | The page is shown inside another page (a preview, for example). Open it through `http://localhost:8000/…`. |
| "MIDI access denied" | Click the icon to the left of the address → Site settings → MIDI devices → Allow, then reload the page. |
| No MIDI ports in the list | The computer can't see the interface. On a Mac, look in Audio MIDI Setup → MIDI Studio. |
| **Detect** gets no reply | Check that the cables run both ways and that **MIDI Filter EX = ENA**. |
| The sound changes badly or in jumps | Raise the **Delay** in the SysEx window. |

## Technical notes

Korg SysEx messages, Model ID `36h`:

| Function | Message |
|---|---|
| Enter Program edit | `F0 42 3n 36 4E 03 00 F7` |
| Change one parameter | `F0 42 3n 36 41 aL aH vL vH F7` (14-bit address and value; negative values in two's complement) |
| Request current sound / reply | `F0 42 3n 36 10 F7` → `40h`, 164 bytes packed 7→8 bits (194 bytes in total) |
| Full bank | request `1Ch`, reply `4Ch` (100 × 164 bytes, 18,750 bytes in total) |
| Write | `F0 42 3n 36 11 00 pp F7` |

`n` = MIDI channel − 1.

## Translations

English is written directly in `x5studio.html`. Each other language is one file in `lang/`:

```
x5studio.html
lang/
  fr.js   it.js   es.js   de.js
```

Each file maps every English text of the interface to its translation, and also holds the "?" help window. To fix a translation, edit the right file. To add a language:

1. copy `lang/fr.js` to `lang/xx.js` (`xx` = the language code, for example `pt`);
2. change `code` and `name` at the top, then translate the right-hand side of each line and the help;
3. add `<script src="lang/xx.js"></script>` next to the other language lines in the `<head>` of `x5studio.html`.

Keep the `{0}`, `{1}` placeholders and the HTML tags as they are. A missing text is simply shown in English.

## Acknowledgements

The parameter map is based on a study of Mauro De Carolis's "05R/W" Ctrlr panel (fixing several encoding errors along the way), checked against the Korg X2/X3 reference manual, then corrected using the official X5DR MIDI implementation tables transcribed in Mark Baylis's [x5dr-editor](https://github.com/Baylo1/x5dr-editor) (MIT License). The edit-mode handling (handing control back to the synth, recovery after a rejected change) follows the behaviour documented in that project. For editing Combinations, Multi, Global and drum kits, that editor is a good complement to X5 Studio.

## Copyright

© 2026 Benjamin PATY (BenjaminPaty54). Released under the [MIT License](LICENSE): you are free to use, modify and share this software, provided you keep the copyright notice.

Korg, X5, X5D, X5DR and 05R/W are trademarks of Korg Inc. This project is independent and is neither affiliated with nor endorsed by Korg.
