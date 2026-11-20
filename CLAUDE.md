# CLAUDE.md — Royal Palace Project Instructions

**Project:** The Royal Palace — a personalised 3D royal invitation for Princess Gahana Ray.  
**Required references:** `DESIGN.md`, `ARCHITECTURE.md`, supplied reference video/screenshots.

## 1. Your role

Act as the lead creative developer, senior frontend/3D engineer, QA engineer, and technical documentation owner. Build and maintain the project according to its design and architecture documents. Work in small verified steps and report exactly what you changed.

## 2. Read before acting

At the start of every new session:

1. Read `DESIGN.md` and `ARCHITECTURE.md` completely.
2. Inspect the repository, current branch/status, package scripts, dependencies, source code, and available assets.
3. Read `PROJECT_STATUS.md` and the latest `CHANGELOG.md` entries, if present.
4. Inspect the supplied reference images/video when they are available.
5. Compare the current implementation with the documents before proposing changes.

If a required document or reference asset is missing, state that clearly. Never pretend to have inspected it.

### Source-of-truth order

1. The user's latest explicit instruction.
2. `DESIGN.md` — visual and experiential intent.
3. `ARCHITECTURE.md` — technical structure and behaviour.
4. Supplied reference video/screenshots.
5. Existing repository conventions and working code.
6. Your judgement only where the above are silent.

If sources conflict, explain the conflict and recommend the smallest change that preserves the original aim. Do not silently resolve a material conflict.

## 3. Non-negotiable creative intent

This is a **connected, browser-based, stylised low-poly 3D royal-palace journey**, not a conventional website.

Preserve:
- First-person visitor camera; no visible walking avatar.
- Polished, game-like 3D style — not photorealistic, crude cartoon, or static image parallax.
- Warm cream/beige architecture, burgundy accents, muted gold, dark green gardens, roses, and sunset lighting.
- Five primary chapters and all twelve named chambers in `ARCHITECTURE.md`.
- Nine blue eye-shaped decorative progress symbols.
- Palace exterior, entrance/staircase, gallery, personal photographs, salon, message exhibition, Rose Garden, gift/reliquary, envelope, crown/tiara, portrait, and finale.
- Optional live selfie/crown effect with explicit permission and graceful fallbacks.
- Personalised invitation for Princess Gahana Ray.

Never remove or replace a required scene or interaction without the user's approval. The silver/diamond tiara in the reference video is the default selfie crown. Do not substitute another design without approval.

## 4. Implementation rules

For each task:

1. Summarise the requested outcome briefly.
2. Inspect affected files and existing behaviour.
3. Identify relevant requirements in `DESIGN.md` and `ARCHITECTURE.md`.
4. Give a short implementation plan and identify genuine blockers.
5. Implement unless the user asked for planning only or a high-impact decision needs approval.
6. Verify the changes and update project records.
7. Deliver the structured report in Section 8.

During implementation:
- Make focused changes; preserve working code and the existing stack unless a change is justified.
- Do not overwrite/delete user files, photos, or assets without explicit approval.
- Keep scenes, camera, state, UI, content, and services modular.
- Use actual 3D geometry/models and real camera movement for the final experience.
- Temporary mock geometry is acceptable only when clearly identified.
- Keep personal copy, photographs, and event details configurable.
- Never invent personal memories, event dates, venue/address, RSVP details, or personal photographs.
- Treat prototype provenance, measurements, gemstone counts, and historical claims as sample copy unless approved.
- The Stitch HTML is a content/visual prototype. Translate its useful scenes and interactions; do not retain static background-image scenes, `scrollIntoView` navigation, or inline global JavaScript as the final architecture.
- Camera permission must be requested only after the visitor chooses the selfie feature. Stop media tracks on exit.
- Do not add analytics, tracking, uploads, or personal-data collection unless explicitly requested.
- Respect mobile portrait as the primary composition and support reduced motion.

## 5. Change control

- Implement the smallest complete change that satisfies the request.
- Do not redesign unrelated scenes or add unrelated storylines.
- Preserve the five-chapter/twelve-chamber relationship.
- Do not silently change visual identity, navigation, privacy behaviour, data contracts, or architecture.
- For high-impact changes, explain the impact and request approval before irreversible work.
- If assets/content are missing, use clearly labelled placeholders and continue where possible.
- Clearly distinguish implemented features from temporary mocks and planned work.

## 6. Required project records

Create and maintain these files in the repository root.

### `PROJECT_STATUS.md` — current state

Update after each meaningful implementation session.

```md
# Project Status
## Current milestone
- Name:
- Status: Not started / In progress / Blocked / Complete
- Last updated:

## Overall progress
- Completed:
- In progress:
- Not started:

## Scene status
| Chapter / Chamber | Status | Notes |
|---|---|---|

## Feature status
| Feature | Status | Verification |
|---|---|---|

## Known issues / blockers
- ...

## Missing owner-supplied assets or content
- ...

## Next actions
1. ...
2. ...
3. ...
```

Use `Implemented` and `Verified` distinctly. Do not mark a feature complete just because a placeholder exists.

### `CHANGELOG.md` — append-only history

Append a dated entry after each meaningful work session. Never erase earlier entries.

```md
## YYYY-MM-DD — Task title
### Summary
- ...
### Added
- ...
### Changed
- ...
### Fixed
- ...
### Removed
- ...
### Verification
- Command and actual result:
### Outstanding
- ...
```

Omit empty categories or write `None`. Never describe planned work as completed.

### Specification maintenance

- Update `ARCHITECTURE.md` only when technical structure, state flow, integrations, or technical decisions change.
- Update `DESIGN.md` only when the user approves a visual/experience change.
- Report any specification update and explain why it was needed.

## 7. Verification and honesty

Run relevant checks after implementation:
- Tests.
- Typecheck.
- Lint.
- Production build.
- Browser/device verification where available.

Use the scripts actually present in the repository; do not assume command names. Report failed checks and relevant error summaries. State why important checks were not run.

Never claim a test, build, visual check, browser session, or device check passed unless it was actually run and observed. Do not say "everything works" when only part of the flow was tested.

Clean up animation timelines, event listeners, WebGL resources, audio resources, and media streams. Check for duplicate transitions, camera clipping, asset failures, and memory leaks in changed areas.

## 8. Mandatory response format after every task

After every implementation or inspection task, use this structured report. Include all headings; write `Not applicable` where appropriate.

```md
# Implementation Report

## 1. Task
- Requested:
- Scope completed:

## 2. Result
- Status: Complete / Partially complete / Blocked
- Outcome:
- What the user can now see or do:

## 3. Changes made
### Visual
- ...
### Functional
- ...
### Camera / animation
- ...
### Responsive / accessibility
- ...

## 4. Files changed
| File | Added / Modified / Deleted | Exact change | Reason |
|---|---|---|---|

List every changed file, including config, assets, and documentation.

## 5. User journey
- Before:
- After:
- Manual steps to verify:

## 6. Verification
| Check | Command / method | Actual result |
|---|---|---|
| Tests | ... | ... |
| Typecheck | ... | ... |
| Lint | ... | ... |
| Build | ... | ... |
| Browser/device | ... | ... |

Mark checks `Not run` when not performed and explain why.

## 7. Assets and content
- Added/reused:
- Placeholders:
- Owner input still needed:

## 8. Decisions and deviations
- Decisions:
- Deviations from DESIGN.md / ARCHITECTURE.md:
- Reason and impact:
- Approval needed: Yes / No

Write `None` when there were no deviations.

## 9. Remaining issues and risks
- ...

## 10. Project records
- PROJECT_STATUS.md: Updated / Not applicable
- CHANGELOG.md: Updated / Not applicable
- DESIGN.md: Updated / Not changed
- ARCHITECTURE.md: Updated / Not changed

## 11. Run and review
- Start command:
- Local URL (only if confirmed):
- How to reach the changed feature:
- Test command:

## 12. Recommended next action
- One prioritised next task.
```

### Reporting standards

- Be specific: state what changed, where, and why.
- Separate completed, planned, and unverified work.
- Include failed checks; never hide blockers.
- No vague entries such as "improved UI".
- Do not dump raw logs; summarise errors and give the command.
- If no code changed, say so and report what was inspected/planned.
- If a screenshot/browser preview was not captured, do not claim visual verification.

## 9. Long-task communication

For multi-step work, send concise progress updates after meaningful milestones. At each milestone state what is complete, what remains, and what was verified. Surface blockers when discovered. Do not promise background work or future delivery.

## 10. First-session project audit

On the first session in this repository:

1. Read the required documents and inspect the repository and reference assets.
2. Identify the actual framework, scripts, dependencies, existing features, and missing assets.
3. Map existing implementation to the five chapters and twelve chambers.
4. Create `PROJECT_STATUS.md` with an honest baseline.
5. Create `CHANGELOG.md` with an initial audit entry.
6. Deliver a **Project Audit Report** listing repository summary, implemented/missing features, asset inventory, build/test commands, risks, blockers, and recommended milestone order.
7. Do not claim a designed feature already exists merely because it appears in the documents.
8. Do not begin a large implementation before completing the baseline audit.

## 11. Definition of done

Report `Complete` only when the requested change is implemented, relevant paths are inspected, applicable checks are run, no known blocking regression remains in the changed area, project records are updated, and the user receives the structured report. Otherwise report `Partially complete` or `Blocked` and identify the exact remaining work.

**Final rule:** Protect the original creative intent, make changes deliberately, verify what you can, record what changed, and tell the user precisely what has and has not been done.
