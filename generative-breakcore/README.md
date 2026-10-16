# Generative Breakcore — BespokeSynth starter patch

An infinite, never-repeating breakcore patch for
[BespokeSynth](https://github.com/BespokeSynth/BespokeSynth), built from its
own generative modules. No samples of ours — it uses Bespoke's bundled 808 kit.

## The patch

```
transport (174 BPM)
├── breaks ── euclideansequencer ──→ kit (drumplayer, 808 kit) ──→ drumbus ──┐
├── ghosts ── randomnote ──→ ghostchance ──→ kit (ghost hits / fills) ───────┤
├── bassline ── randomnote (D1) ──→ reese (fmsynth sub) ──→ bassbus ─────────┤
└── chaos ── lfo (unpatched — wire it yourself, see below)                   │
                                                                             ▼
                                                     drumbus + bassbus ──→ master ──→ splitter ──→ output 1/2
```

- **breaks**: 4 euclidean rings firing the drum kit. Hit the `random` button on
  the module for a brand-new rhythm; the `steps`/`onsets`/`rot` randomizers
  re-roll sections of it.
- **ghosts**: probabilistic 16th-note ghost hits through a chance gate —
  this is where the fill/burst energy comes from.
- **bassline**: rolling D1 sub pulses into a detuned FM bass.
- **chaos**: a free LFO. Cable it to `ghostchance`'s chance slider, the master
  gain, or a filter cutoff and the patch starts breathing on its own.

## How to load it

1. Build (or download) BespokeSynth from this repo.
2. Copy `breakcore-starter.json` into your BespokeSynth `layouts` folder
   (inside the user data directory Bespoke creates on first run).
3. In Bespoke, open the title bar menu → layouts → `breakcore-starter`.
4. Press play on the transport. It will not repeat itself.

## Tweaking it live (the DJ part)

- Ride `master` gain and the bus gains like a mixer.
- Euclidean rings: change steps/onsets live — the rhythm morphs without stopping.
- `random` on the euclidean sequencer = instant new break.
- Cable `chaos` (LFO) to anything with a slider to make the patch perform itself.
- Swap the drumplayer's 808 samples for your own break chops.

## Format notes

This is a Bespoke layout JSON (`{modules, zoomlocations}`). Each module entry is
`{name, position, type, target}` where `target` is a comma-separated list of
module names the module's main output cable connects to (`target2` for a second
output, e.g. splitter). Module-specific params use the modules' own save keys.
