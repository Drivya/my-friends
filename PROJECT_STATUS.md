# Project Status

## Current milestone
- Name: Milestone 0 — Repository audit (ARCHITECTURE.md §19)
- Status: Complete (audit only; no application code exists yet)
- Last updated: 2026-11-20

## Overall progress
- Completed:
  - First-session project audit.
  - Specification documents committed to the repository root (`CLAUDE.md`, `DESIGN.md`, `ARCHITECTURE.md`), byte-identical to the uploaded files.
  - Project records created (`PROJECT_STATUS.md`, `CHANGELOG.md`).
- In progress:
  - None.
- Not started:
  - Everything in Milestones 1–8: application scaffold, state model, overlay UI, all 12 chambers, camera rig, modals, envelope, crown, selfie camera, finale, audio, tests, build.

### Baseline: what the repository actually contains
| Path | What it is | Relation to the Royal Palace project |
|---|---|---|
| `vault-door/index.html` | Standalone 880-line Three.js r160 demo ("How a vault door locks"), loaded via CDN import map, Google Fonts, no build step | **Unrelated.** Not part of this project. Left untouched. Nothing reusable beyond general technique (timeline-driven camera, reduced-motion check). |
| `CLAUDE.md`, `DESIGN.md`, `ARCHITECTURE.md` | Project specifications (added this session) | Source of truth for the build. |
| `PROJECT_STATUS.md`, `CHANGELOG.md` | Project records (added this session) | Required by `CLAUDE.md` §6. |

There is no `package.json`, no `src/`, no `public/`, no assets, no tests, no build tooling, no CI config, no README.
Git: one commit (`8e49bf9`, vault door). Branches `claude/gallant-volta-x10dod` (working branch) and `claude/prompt-analysis-rf2tve` point to the same commit.

## Scene status
| Chapter / Chamber | Status | Notes |
|---|---|---|
| 01 The Arrival — I Grand Facade | Not started | Palace façade, formal garden, dusk sky, opening invitation copy |
| 02 The Grand Entrance — II Portal | Not started | Walnut double doors with hinge animation |
| 02 The Grand Entrance — III Welcome Hall / Rotunda | Not started | Reference staircase, burgundy runner, checkered floor, chandelier |
| 03 The Royal Gallery — IV Museum Gallery | Not started | Vaulted corridor, chandeliers, burgundy walls, runner |
| 03 The Royal Gallery — V Memory Exhibition | Not started | Blocked on owner photographs for final content |
| 04 The Grand Ballroom — VI Private Salon | Not started | Spec conflict with DESIGN.md ballroom — see Known issues #1 |
| 04 The Grand Ballroom — VII Message Exhibition | Not started | Default plaque copy available from DESIGN.md |
| 05 The Rose Garden — VIII Gardens | Not started | Default line "Every rose here is yours." |
| 05 The Rose Garden — IX Gift / Reliquary + Envelope | Not started | Envelope is required; casket optional — see Known issues #4 |
| 05 The Rose Garden — X Crown | Not started | Setting conflict — see Known issues #2; tiara asset missing |
| 05 The Rose Garden — XI Portrait | Not started | Needs owner portrait or selfie output |
| 05 The Rose Garden — XII Finale | Not started | Guestbook client-side only, truthful confirmation |

## Feature status
| Feature | Status | Verification |
|---|---|---|
| App shell, canvas, error boundary, loading state | Not started | — |
| Typed experience state (5 chapters / 12 chambers / reveal sub-states) | Not started | — |
| Chapter header + five-chapter progress | Not started | — |
| Nine blue eye motif | Not started | — |
| Sound toggle / AudioController | Not started | No audio assets supplied |
| Imperial Navigator (desktop, optional) | Not started | — |
| Camera rig + waypoints | Not started | — |
| Content configuration layer | Not started | — |
| Memory modal | Not started | — |
| Gift ledger panel | Not started | — |
| Envelope open animation + invitation details | Not started | No event details supplied |
| Crown reveal + inspection modal | Not started | — |
| Selfie camera + face-tracked tiara | Not started | — |
| Guestbook | Not started | — |
| WebGL / asset / camera / audio fallbacks | Not started | — |
| Reduced motion, safe areas, keyboard access | Not started | — |
| Unit / integration / e2e tests | Not started | — |
| Production build | Not started | — |

## Known issues / blockers
1. **Spec conflict — Chapter 04 content.** DESIGN.md describes one ballroom (parquet, chandelier, flower arrangements, plaque "A little kingdom, made for one very special girl"). ARCHITECTURE.md splits it into Chamber VI (walnut-panelled salon with fireplace) and Chamber VII (burgundy "Proclamation" stele with multi-paragraph decree). Recommendation: Chamber VI = a short, restrained salon antechamber in the shared palette; Chamber VII = the reference ballroom, with the DESIGN.md plaque copy as the default and the decree fields optional/blank. **Needs owner approval.**
2. **Spec conflict — crown setting.** DESIGN.md §4 says the garden stays behind the envelope and crown states; ARCHITECTURE.md Chamber X describes a crown room/rotunda. Recommendation: place the crown pedestal inside the garden's domed gazebo at dusk — a rotunda that keeps the garden behind it and gives the darker, intimate lighting the reference shows. **Needs owner approval.**
3. **Scope difference — final sequence.** DESIGN.md: Envelope → Crown → Camera → Completion. ARCHITECTURE.md/CLAUDE.md add Gift ledger, Crown inspection, Portrait chamber, Finale + guestbook. CLAUDE.md §3 requires all twelve chambers, so the plan follows ARCHITECTURE.md with these nested inside Chapter 05 (no new top-level chapters). Recorded, not blocking.
4. **Gift casket vs envelope.** The personal envelope is required. Whether the Stitch prototype's gift casket is also shown is an owner decision. Default plan: envelope only, ledger panel attached to the envelope pedestal. **Needs owner decision.**
5. **Token mismatch.** ARCHITECTURE.md §7.6 says the "Palatial Heritage" tokens come from DESIGN.md, but the supplied DESIGN.md does not contain them (they appear only in ARCHITECTURE.md). UI text/hairline values also differ (`#F6EEE5`/`#B89A62` in DESIGN vs `#F4EBDD`/`#9A8F80` in ARCHITECTURE). Plan: DESIGN.md values for the in-scene overlay (DESIGN.md ranks higher), ARCHITECTURE.md dark tokens for modals/panels.
6. **Reference media not supplied.** No screenshots, no 79-second video, and no Stitch HTML prototype are in the repository or this session's uploads. Scene composition cannot be checked against the visual source of truth (DESIGN.md §2 priority 1). **Blocks visual fidelity verification.**
7. **Project location undecided.** The repo already holds an unrelated `vault-door/` demo. Recommendation: build the app in a `royal-palace/` subfolder with its own `package.json`, leaving `vault-door/` untouched. Specs/records stay at the repo root. **Needs owner approval.**

## Missing owner-supplied assets or content
- Reference screenshots (all five chapters + envelope + crown + selfie) and the 79-second reference video.
- Stitch HTML prototype export (twelve-chamber copy, navigator, modals).
- Personal gallery photographs, each with title, optional caption/record label, and alt text.
- Final portrait image (Chamber XI), or confirmation that the selfie output is the portrait.
- Event details: title, date, time, venue, address, dress code, RSVP, additional message.
- Finale heading and closing message.
- Silver/diamond tiara: 3D model (GLB) and a 2D/3D overlay asset for the selfie. If none is supplied, a procedural tiara will be built and labelled as such.
- Optional: background music and sound effects (with licence).
- Optional: royal crest/monogram.
- Optional: hero models (palace, doors, chandelier, fountain, gazebo, envelope). If not supplied, procedural low-poly geometry will be used.
- Confirmation of the nine blue eye symbol design (custom SVG, or owner-supplied icon).

## Next actions
1. Owner decisions: issues #1, #2, #4, #7 above, plus confirmation of the proposed stack.
2. Owner uploads the reference screenshots/video and the Stitch HTML.
3. Milestone 1 — runtime foundation: Vite + React + TypeScript scaffold, typed state, content layer, overlay UI (header, progress, nine eyes, sound toggle), error/WebGL fallback, Vitest unit tests, first production build.
