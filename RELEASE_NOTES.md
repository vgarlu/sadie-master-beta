First public beta of **SadieMaster** — a native Apple Silicon reimplementation of the SADiE 6
mastering workflow, built from Prism's published SADiE 6 manual rather than from SADiE code.

**macOS 14+ on Apple Silicon only** (arm64; no Intel build).

### First launch
The build is ad-hoc signed, not notarized, so macOS blocks the first double-click. Either
right-click the app → **Open** → **Open**, or run once:

```bash
xattr -dr com.apple.quarantine /Applications/SadieMaster.app
```

### In the zip
- `SadieMaster.app` — version 0.4.0 (build 4)
- `Demo/Demo Mastering.sadieproj` + media — three edited tracks, opens in a second
- `HOW TO OPEN.txt` — the same instructions in English and Spanish

### What's working
- EDL editing: streams, clips with source in/out, razor cuts, splice (overlap) and V-cut
  crossfades, per-entry trims and fades, slip editing, 3- and 4-point edits, 50-level undo
- 117 fade shapes across the linear / cos / cosh / exp / log / pow / S families
- PQ list at 75 fps with offsets, validation, ISRCs, CD Text, CUE export
- Broadcast WAV master with bext + iXML metadata, 16/24-bit, TPDF or shaped dither
- WAV Master: one BWF per PQ track using `<Tag>` naming
- Sample-accurate mixer rendering a 60-minute programme in seconds

### Verified in this build
- Build: 0 warnings, 0 errors; `codesign --verify` passes after unzipping; arm64 thin
- Engine selftest: 37/37 checks
- Offline render: ~1671× realtime; 24-bit render matches the mixer to 1.2e-07
- Interface contrast measured on the rendered build: 12.9:1 on the inspector tabs, 11.4–11.6:1
  on card text

### Not in yet
DDP output (deliberately deferred until it can be validated against an independent reader — do
not send a beta render to a pressing plant), EQ/dynamics/plugins, automation, surround,
timecode, CD burning.

**Do not use a beta for a real master.** Work on copies of your material.

SHA-256 of the zip:
`0bb7652206960ed34a894a831c28318a46a2c94c83c39ab2a765a78fe2f1232c`
