# Project Status

## Current milestone
- Name: Milestone 0 — Repository audit (ARCHITECTURE.md §19), second pass with reference material
- Status: Complete (audit only; no application code exists yet)
- Last updated: 2026-11-20

## Overall progress
- Completed:
  - Audit of the repository, the specs, the Stitch export and 8 unique reference screenshots.
  - Specs committed at the root (`CLAUDE.md`, `DESIGN.md`, `ARCHITECTURE.md`). Amended once, by owner instruction, to remove the nine-eye motif.
  - Stitch export committed to `stitch-export/`.
  - Written scene catalogue in `references/README.md` (images withheld: the repository is public).
- In progress:
  - None.
- Not started:
  - Everything in Milestones 1–8: application scaffold, state model, overlay UI, all 12 chambers, camera rig, modals, envelope, crown, selfie camera, finale, audio, tests, build.

### What the repository contains
| Path | What it is | Status |
|---|---|---|
| `CLAUDE.md`, `DESIGN.md`, `ARCHITECTURE.md` | Project specifications | Committed; amended for the eye-motif removal |
| `PROJECT_STATUS.md`, `CHANGELOG.md` | Project records | Maintained |
| `references/README.md` | Text catalogue of the reference screenshots | New |
| `stitch-export/code.html` | Stitch prototype: 986 lines; Tailwind CDN; 12 sections; inline global JS | Reference only — not final architecture |
| `stitch-export/DESIGN.md` | Stitch "Palatial Heritage" tokens: colours, Playfair Display / Newsreader type scale, elevation, buttons | Reference for modal/panel styling |
| `stitch-export/screen.png` | 189×1600 full-page thumbnail of the prototype | Reference only |
| `vault-door/index.html` | Unrelated Three.js demo | Untouched; not part of this project |

The following do not exist: `package.json`, `src/`, `public/`, `assets/`, a reference video, `README.md`, tests, CI.

### Stitch export: what is usable
- **Usable:**
  - Chamber order and names (I–XII).
  - Navigator labels: Facade, Portal, Rotunda, Gallery, Memories, Salon, Stele, Parterre, Reliquary, Crown, Portrait, Finale.
  - Modal patterns: memory, crown inspection.
  - Gift-ledger toggle, guestbook flow, "Palace Resonance" label.
  - Design tokens.
  - The JS behaviours, which map one-to-one to ARCHITECTURE.md §11.3.
- **Not usable:**
  - All 20 images are hot-linked from `lh3.googleusercontent.com` and some are AI-generated, including a fabricated "princess" portrait (Chamber XI) and fabricated "memory" photos (Chamber V). None may ship.
  - The page loads Tailwind and its fonts from the internet at runtime.
  - The audio toggle is simulated (no sound plays).
  - The crown pane labelled "360 Axis Live View" is a static image.
  - Curatorial copy (dates, measurements, gem counts, provenance) is demo text that needs owner approval before it can be shown.

## Scene status
| Chapter / Chamber | Status | Reference available | Notes |
|---|---|---|---|
| 01 Arrival — I Grand Facade | Not started | Thumbnail only; garden screenshot shows the same château from behind | Need an Arrival still |
| 02 Grand Entrance — II Portal | Not started | No (Stitch text only) | Walnut doors + hinge animation |
| 02 Grand Entrance — III Welcome Hall | Not started | **Yes** (file 4) | Checkerboard floor, runner stair, side flights, finials, chandelier |
| 03 Royal Gallery — IV Museum Gallery | Not started | **Yes** (file 3) | Barrel vault, chandeliers, burgundy walls, parquet + runner |
| 03 Royal Gallery — V Memory Exhibition | Not started | **Yes** (file 2 frame close-up) | Blocked on original photos |
| 04 Grand Ballroom — VI Private Salon | Not started | No (Stitch text only) | See decision D1 |
| 04 Grand Ballroom — VII Message Exhibition | Not started | **Yes** (file 1) | The reference ballroom; "TAP TO READ" long message needed |
| 05 Rose Garden — VIII Gardens | Not started | **Yes** (files 5, 7) | Château backdrop, gazebo, rose beds, topiary |
| 05 Rose Garden — IX Reliquary / Envelope | Not started | **Yes** (file 9) | Table in gazebo: envelope with wax seal, candles, roses |
| 05 Rose Garden — X Crown | Not started | **Yes** (file 8) | Tiara on tufted cushion, pedestal beside the envelope table in the gazebo |
| 05 Rose Garden — XI Portrait | Not started | Selfie thumbnail only | Needs owner portrait or selfie output |
| 05 Rose Garden — XII Finale | Not started | No (Stitch text only) | Guestbook client-side only |

## Feature status
| Feature | Status | Verification |
|---|---|---|
| App shell, canvas, error boundary, loading state | Not started | — |
| Typed experience state (5 chapters / 12 chambers / reveal sub-states) | Not started | — |
| Chapter header (label · counter, five-dash progress, back, sound) | Not started | Reference fully documented |
| ~~Nine blue eye motif~~ | Removed by owner instruction 2026-11-20 | Not applicable |
| Sound toggle / AudioController | Not started | No audio assets |
| Imperial Navigator (desktop, optional) | Not started | — |
| Camera rig + waypoints | Not started | — |
| Content configuration layer | Not started | — |
| Memory modal | Not started | — |
| Ballroom "tap to read" message view | Not started | Owner text missing |
| Gift ledger panel | Not started | See decision D3 |
| Envelope open animation + letter + invitation details | Not started | Owner text missing |
| Crown reveal + inspection modal | Not started | — |
| Selfie camera + face-tracked tiara (incl. "Waiting for the camera…" state) | Not started | — |
| Guestbook | Not started | — |
| WebGL / asset / camera / audio fallbacks | Not started | — |
| Reduced motion, safe areas, keyboard access | Not started | — |
| Tests / build | Not started | — |

## Decisions
### Resolved by evidence (no approval needed)
- **R1 – Crown setting:** the tiara pedestal stands inside the garden gazebo, beside the envelope table (files 8, 9). This matches DESIGN.md, and ARCHITECTURE.md's "domed rotunda" is satisfied by the gazebo.
- **R2 – Chamber VII:** it is the reference ballroom (file 1), with the plaque copy from DESIGN.md. Its far door is signed "The Rose Garden".
- **R3 – Token source:** "Palatial Heritage" tokens are in `stitch-export/DESIGN.md`.
  - DESIGN.md scene palette: 3D world and in-scene overlay.
  - Palatial Heritage: modals and panels.
- **R4 – Where reference and Stitch differ, the reference wins** (DESIGN.md §2):
  - Gallery floor is parquet + runner, not checkerboard.
  - Staircase is cream stone + burgundy runner, not rouge marble.
  - The palace is a French château with mansard roofs, not the Stitch stock-photo palace.
- **R5 – Eye motif:** removed by owner instruction; specs amended.

### Awaiting owner decision
- **D1 – Chamber VI (Private Salon)** has no reference.
  - Recommend: a short, restrained antechamber between the gallery and the ballroom, in the reference palette (cream panelling, burgundy upholstery, a fireplace). No Stitch provenance text.
- **D2 – Typography.** The reference uses an italic old-style serif for messages and a light, wide-tracked geometric sans for labels. ARCHITECTURE.md/Stitch name Playfair Display + Newsreader.
  - Recommend: match the reference with locally bundled OFL fonts — Cormorant Garamond for the name and messages, Jost (or similar) for labels.
  - Keep Newsreader only for long modal body text, or drop it.
- **D3 – Gift casket.** The reference shows no casket.
  - Recommend: no casket. Chamber IX is the gazebo envelope table; the "ledger" becomes optional detail text on the envelope.
- **D4 – Privacy / repository visibility.** `Drivya/my-friends` is public. Personal photos, the letter, the event address and RSVP details committed here would be public, and stay in git history.
  - Recommend: make the repository private before Milestone 3, or keep personal content in a git-ignored folder supplied at deploy time.
- **D5 – Project location.** Recommend `royal-palace/` subfolder; leave `vault-door/` untouched.
- **D6 – Stack confirmation:**
  - Vite + React + TypeScript
  - three + React Three Fiber + Drei
  - GSAP; Zustand
  - Vitest + Playwright
  - MediaPipe Tasks Vision, bundled locally

## Known issues / blockers
1. No reference video in the repository or uploads. Camera motion timing and transitions can only be inferred from stills.
2. Missing stills: Arrival (Chapter 01), the opened letter, the ballroom long message, the live selfie view.
3. Owner text visible but illegible in the screenshots:
   - Garden sky message ("Happy B…").
   - Gallery end-door sign.
   - Ballroom "tap to read" content.
   - Letter content.
4. `README.md` named as a mandatory handoff document, but none was supplied.

## Missing owner-supplied assets or content
- **References:**
  - The reference video.
  - Arrival screenshot; screenshots of the letter, the ballroom message page and the selfie view.
- **Photos and portrait:**
  - Original gallery photographs, each with title, optional caption and alt text. State how many frames are wanted.
  - Final portrait (Chamber XI), or confirmation that the selfie is the portrait.
- **Text:**
  - Ballroom long message (behind "TAP TO READ").
  - Garden sky message (exact text).
  - Gallery end-door sign text.
  - Envelope letter text.
  - Event details: title, date, time, venue, address, dress code, RSVP, extra message. Only the fields you supply will be shown.
  - Finale heading and closing message.
- **Models and audio:**
  - Tiara: GLB model and/or transparent PNG for the selfie overlay. Otherwise a procedural tiara will be built from the file 8 reference and labelled as such.
  - Optional: licensed background music and sound effects.
  - Optional: crest/monogram.
  - Optional: palace, chandelier, gazebo or envelope models. Otherwise procedural low-poly geometry.
- **Handoff:** `README.md`, if one exists.

## Next actions
1. Owner: decide D1–D6 (D4 first).
2. Owner: supply the reference video, the missing stills and the text items listed above.
3. Milestone 1 — runtime foundation:
   - scaffold, typed state, content layer;
   - header with five-dash progress and sound toggle;
   - WebGL fallback, unit tests, first production build.
   It needs no personal content.
