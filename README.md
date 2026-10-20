# SadieMaster — beta builds

Download-only repository for **SadieMaster**, a native Apple Silicon reimplementation of the
SADiE 6 mastering workflow (EDL playlist editing, PQ/CD mastering, Broadcast WAV delivery).
The source lives in a private repository; this repo exists so beta testers can get a build
without a GitHub account or repository access.

## Download

Latest beta: **[Releases →](../../releases/latest)**

| Version | Build | Size | SHA-256 |
|---|---|---|---|
| 0.5.0-beta.1 | 5 | 15.3 MB | `47fef099784cca10a2ef28a806b7b3a55d4dbfcbe1d9972c2726b6c941d893e7` |
| 0.4.0-beta.1 | 4 | 15.2 MB | `0bb7652206960ed34a894a831c28318a46a2c94c83c39ab2a765a78fe2f1232c` |

Requirements: **macOS 14 (Sonoma) or newer on Apple Silicon** (M1 and later). The binary is
arm64 only — it will not run on Intel Macs.

## First launch

The build is ad-hoc signed, not notarized by Apple, so the first double-click is refused.
Either right-click the app → **Open** → **Open**, or run once:

```bash
xattr -dr com.apple.quarantine /Applications/SadieMaster.app
```

The zip contains `HOW TO OPEN.txt` with the same instructions, plus a ready-made demo project
(`Demo/Demo Mastering.sadieproj`) so you can test in under a minute: open it, press **⌘G** to
generate the PQ list, **⌘B** to render a master.

## What to test

- Import your own audio (**⌘I**): WAV/AIFF/CAF/FLAC/MP3/M4A at any sample rate
- Razor at playhead (**⌘K**), splice and V-cut crossfades, trimming clip edges
- Undo/redo, scrubbing the ruler, zoom, playback while editing
- PQ: generate, edit titles and ISRCs, validation warnings, CUE export
- Render master at 16-bit with dither; WAV Master (one file per PQ track)
- **DDP 2.00 fileset** (0.5.0+): `Delivery → DDP Fileset…` (⇧⌘D), or
  `sadiex ddp project.sadieproj --out DIR`; check it with `sadiex ddpverify DIR`

## Known gaps

Not bugs — not built yet:

- **DDP output is beta.** It writes a complete DDP 2.00 fileset and verifies it internally, but no
  pressing plant has ingested one yet and no third-party DDP tool has read one. Inspect the PQ
  sheet, and keep a WAV + CUE fallback for a first real delivery.
- No EQ, dynamics, plugin hosting, automation, surround or timecode.
- No CD burning (modern macOS cannot).

**Do not use a beta for a real master.** Work on copies of your material.

## Reporting

Say what you did, what you expected and what happened, plus your macOS version and Mac model.
A screenshot — and the `.sadieproj` if it reproduces — helps a lot.
