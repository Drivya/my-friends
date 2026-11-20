# Changelog

Append-only. Newest entries at the bottom.

## 2026-11-20 — First-session project audit (Milestone 0)
### Summary
- Audited the repository against `CLAUDE.md`, `DESIGN.md` and `ARCHITECTURE.md`. The repository contains no Royal Palace implementation; the only existing code is an unrelated standalone Three.js demo, `vault-door/index.html`.
- No application code was written.
### Added
- `CLAUDE.md`, `DESIGN.md`, `ARCHITECTURE.md` — the uploaded specifications, copied byte-for-byte into the repository root (SHA-256 verified against the uploads) so later sessions can read them as `CLAUDE.md` §2 requires.
- `PROJECT_STATUS.md` — baseline status: all 5 chapters, 12 chambers and all features "Not started"; spec conflicts, blockers and missing assets recorded.
- `CHANGELOG.md` — this file.
### Changed
- None.
### Fixed
- None.
### Removed
- None. `vault-door/` left untouched.
### Verification
- `git status`, `git log --all`, `git ls-tree` on both branches: one commit (`8e49bf9`), one file (`vault-door/index.html`); both branches identical.
- `find` over the working tree: no `package.json`, `src/`, `public/`, assets, tests or CI config.
- `sha256sum` of the copied spec files matched the upload manifest.
- Toolchain check: Node v22.23.5, npm 10.9.9, npm registry reachable (`three` 0.187.0, `@react-three/fiber` 9.8.2, `@mediapipe/tasks-vision` 1.2.3 resolvable), Playwright importable.
- Tests / typecheck / lint / build: not run — no project or scripts exist yet.
### Outstanding
- Owner decisions on Chapter 04 content, crown setting, gift casket, and project location (see `PROJECT_STATUS.md`).
- Reference screenshots/video, Stitch HTML, photographs, event details and tiara asset not yet supplied.
- Milestone 1 (runtime foundation) not started.

## 2026-11-20 — Audit pass 2: Stitch export and reference screenshots
### Summary
- Inspected the uploaded Stitch export (zip: `code.html`, `screen.png`, `DESIGN.md`) and 8 unique reference screenshots (9 files; 5 and 6 identical).
- Found that `/references`, `/stitch-export`, `/assets` and `README.md` (named in the handoff) did not exist in the repository.
- No application code was written.
### Added
- `stitch-export/code.html`, `stitch-export/screen.png`, `stitch-export/DESIGN.md`: the Stitch export, byte-identical to the zip contents.
- `references/README.md`: written catalogue of every screenshot (geometry, materials, light, UI, confirmed copy, video thumbnail order).
### Changed
- `CLAUDE.md` §3, `DESIGN.md` §6.2 / §11 tree / §15 / §16, `ARCHITECTURE.md` §3 / §4 / §7.3 / §14.1 / §18.3 / §21: removed the nine-blue-eye motif requirement. Reason: owner instruction ("ignore the purple eyes"). The row is a video-editing emoji overlay, not part of the product.
- `PROJECT_STATUS.md`: rewritten with per-chamber reference availability, resolved decisions (R1–R5), pending decisions (D1–D6) and the full missing-content list.
### Fixed
- Earlier audit issue "token mismatch": the Palatial Heritage tokens were in the Stitch `DESIGN.md`, now committed.
- Earlier audit issue "crown setting": resolved by screenshots 8 and 9 (tiara pedestal inside the garden gazebo).
### Removed
- None. Reference images were deliberately **not** committed: the repository is public, and the images contain real people's photos and a personal Instagram handle.
### Verification
- `sha256sum` of `stitch-export/*` matches the zip contents.
- Repository visibility checked via GitHub search API: `Drivya/my-friends` is public.
- Spec amendment script asserted exactly one match per replacement; post-edit `grep` shows no remaining eye-motif requirement.
- Tests / typecheck / lint / build: not run (no project exists yet).
### Outstanding
- Owner decisions D1–D6; reference video; missing stills; owner text and photos (see `PROJECT_STATUS.md`).
