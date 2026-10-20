Beta 0.5.0 adds **DDP 2.00 delivery** — the fileset a pressing plant ingests — plus two bug fixes
the work uncovered.

**macOS 14+ on Apple Silicon only** (arm64; no Intel build).

### New: DDP 2.00 fileset
`sadiex ddp "project.sadieproj" --out DIR`, or in the app **Delivery → DDP Fileset… (⇧⌘D)**, writes:

- `IMAGE.DAT` — 2 s pause + programme, 2352-byte sectors, 44.1 kHz / 16-bit little-endian
- `DDPID`, `DDPMS`, `PQDESCR`, `CDTEXT.BIN` (titles and performers, with CCITT CRC16)
- `CHECKSUM.MD5` and a human-readable `PQ_SHEET.TXT`

`sadiex ddpverify DIR` reads a fileset back: packet sizes and markers, image against the map,
PQ monotonicity, lead-out against the image end, CD-Text CRCs and every checksum.

The app verifies the fileset it just wrote before the status bar reports success.

### Fixed
- **CUE and DDP described different discs.** The CUE declared INDEX 00 before tracks 2 and 3; the
  DDP declared none, so a plant cutting from the DDP would have produced a different disc. Both now
  derive pregaps from the same rule, and the selftest asserts they agree.
- **32-bit renders were mislabelled.** The WAV header said PCM (format 1) while the encoder wrote
  Float32. Now correctly declares IEEE float (format 3) — `afinfo` reports `Float32`.

### Verified in this build
- `sadiex selftest`: 53/53 checks; 0 warnings in the release build of both products
- The DDP image's programme section is byte-identical to a 16-bit master rendered by a different
  code path
- Every CUE cue matches its `PQDESCR` packet within one frame; CD-Text CRCs and all MD5s verified
  with independent implementations
- The zip was extracted into a clean directory: signature verifies, version reads 0.5.0, and the
  bundled CLI writes and verifies a fileset from the packaged demo project

### Not verified — read this before sending anything to a plant
**No pressing plant has ingested a fileset yet, and no third-party DDP tool has read one.** The
built-in validator proves the fileset is self-consistent, not that it conforms. Treat DDP output as
beta: try it, inspect the PQ sheet, and keep a WAV+CUE fallback for a first real delivery. Frame
layout and conventions are documented in `docs/DDP.md` in the source repository.

### First launch
The build is ad-hoc signed, not notarized, so macOS blocks the first double-click. Right-click the
app → **Open** → **Open**, or run once:
```bash
xattr -dr com.apple.quarantine /Applications/SadieMaster.app
```

### In the zip
- `SadieMaster.app` — version 0.5.0 (build 5)
- `Demo/Demo Mastering.sadieproj` + media — three edited tracks (note: its track 1 starts 3 s in;
  that audio becomes the track-1 pregap, which the writer reports)
- `HOW TO OPEN.txt` — English and Spanish

SHA-256 of the zip:
`47fef099784cca10a2ef28a806b7b3a55d4dbfcbe1d9972c2726b6c941d893e7`
