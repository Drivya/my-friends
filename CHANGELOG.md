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
