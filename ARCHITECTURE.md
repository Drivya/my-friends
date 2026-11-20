# ARCHITECTURE.md — The Royal Palace Interactive 3D Invitation

**Document type:** Technical architecture and implementation blueprint  
**Project:** The Royal Palace — an interactive digital invitation and heritage journey for Princess Gahana Ray  
**Audience:** Claude Code, frontend/3D developers, and anyone maintaining the project  
**Companion specification:** `DESIGN.md`  
**Primary references:** The supplied 79-second reference video, the supplied mobile screenshots, the existing `Palatial Heritage` design tokens, and the supplied Stitch HTML prototype.

---

## 0. Architectural decision summary

This project is a **real-time, browser-based, stylised 3D experience**. It is not a normal content website, a long scrolling landing page, a static sequence of screenshots, or a hotel/museum marketing template.

The visitor experiences a connected royal world from a first-person camera perspective. They approach the palace, enter, move through its chambers, discover personal photographs and messages, reach the garden, interact with the invitation/envelope, see the crown reveal, and optionally create a final portrait.

### Decisions that must remain true

1. **The 3D world is the product.** The interface is a restrained overlay that guides the visitor.
2. **First-person camera, no visible walking avatar.** The camera represents the visitor.
3. **Stylised low-poly / game-like art direction.** Do not switch to photorealism or crude cartoon styling.
4. **Five primary chapters.** This follows the progress labels in the reference video.
5. **Twelve named chambers.** Preserve the more detailed chamber structure in the Stitch HTML prototype.
6. **Personal content is data-driven.** Photos, messages, event details, and guestbook settings must be replaceable without editing the 3D scene code.
7. **The crown/selfie experience is optional at the camera stage.** Camera permission must never be required to read or complete the invitation.
8. **No invented personal or event facts.** All dates, venues, addresses, RSVP details, photographs, and personal messages must be owner-supplied or clearly marked as development placeholders.
9. **Use the reference screenshots as visual truth.** The HTML export is a more detailed content/prototype reference, not permission to change the look into a static website.
10. **Preserve every meaningful chamber and interaction in the supplied HTML.** Adapt its implementation to the immersive 3D experience instead of dropping content.

---

## 1. Product definition and experience model

### 1.1 Product purpose

Create a personalised royal invitation that feels like entering a beautiful, stylised palace built for one special person. The visit should feel like a short guided adventure with a clear emotional arc:

**Invitation → Arrival → Entry → Discovery → Personal memories → Message → Garden → Gift/envelope → Crown → Portrait → Farewell.**

The experience combines:
- A custom 3D palace and garden.
- First-person cinematic camera movement.
- A small set of clear visitor interactions.
- Personal photography and inscriptions.
- An invitation reveal.
- A crown inspection/reveal.
- An optional live selfie / crown overlay.
- A final dedication and optional guestbook signature.

### 1.2 Two levels of navigation

The reference materials contain two navigation scales. Keep both, but do not confuse them.

**Primary navigation: five chapters** — shown in the mobile-first header, matching the video:

| Chapter | Display title | Main content |
|---|---|---|
| `01 / 05` | THE ARRIVAL | Chamber I — Grand Facade |
| `02 / 05` | THE GRAND ENTRANCE | Chamber II — Portal; Chamber III — Welcome Hall / Rotunda |
| `03 / 05` | THE ROYAL GALLERY | Chamber IV — Museum Gallery; Chamber V — Memory Exhibition |
| `04 / 05` | THE GRAND BALLROOM | Chamber VI — Royal Chamber / Salon; Chamber VII — Message Exhibition |
| `05 / 05` | THE ROSE GARDEN | Chamber VIII — Gardens; Chamber IX — Gift / Reliquary; Chamber X — Crown; Chamber XI — Portrait; Chamber XII — Finale |

This five-chapter grouping is the main progress model for the mobile experience and should read like the five scenes in the supplied video.

**Secondary navigation: twelve named chambers** — derived from the Stitch HTML navigator:

| Roman numeral | Chamber ID | Name in the Stitch prototype | Chapter |
|---|---|---|---|
| I | `chamber-1` | The Grand Facade | 01 |
| II | `chamber-2` | The Grand Royal Entrance / Portal | 02 |
| III | `chamber-3` | The Grand Welcome Hall / Central Rotunda | 02 |
| IV | `chamber-4` | The Royal Museum Gallery / Monumental Enfilade | 03 |
| V | `chamber-5` | The Memory Exhibition / Portrait & Archival Salon | 03 |
| VI | `chamber-6` | The Grand Royal Chamber / Private Sovereign Salon | 04 |
| VII | `chamber-7` | The Royal Message Exhibition / Imperial Proclamation Hall | 04 |
| VIII | `chamber-8` | The Royal Palace Gardens / Formal Parterre | 05 |
| IX | `chamber-9` | The Royal Gift Exhibition / Sovereign Reliquary | 05 |
| X | `chamber-10` | The Grand Royal Crown Room | 05 |
| XI | `chamber-11` | The Final Royal Portrait | 05 |
| XII | `chamber-12` | The Final Palace Experience / Imperial Finale | 05 |

On wide desktop, the twelve-chamber Imperial Navigator can be available as a compact secondary waypoint panel. On mobile it must be collapsed or opened intentionally; it must not occupy the main scene or obscure the chapter indicator. The visitor's guided path remains the default.

### 1.3 Content/reference reconciliation

The supplied video shows five primary chapter labels and a final crown/selfie moment. The Stitch HTML expands the palace into twelve named chambers, including a Welcome Hall, Private Salon, Proclamation Hall, Gift Reliquary, Crown Room, Portrait, and Finale.

Implement this as **five chapters containing twelve chambers**, followed by sub-states inside the final chapter. Do not delete the extra chambers merely to reduce the project to five screens.

The supplied HTML also contains a dark walnut/gold UI system and several elaborate sample curatorial descriptions. Keep the visual tokens and useful layout/content structure, but treat precise historic-sounding claims, dates, measurements, gemstone counts, and provenance statements as editable fictional/demo copy unless the owner explicitly approves them. Do not present unverified specifications as facts.

---

## 2. Technical stack and runtime

### 2.1 Preferred stack

Use the existing repository's stack if one is already installed and working. Do not migrate frameworks without a strong reason. If the repository is new, use:

- **React** — UI composition and application state.
- **TypeScript** — typed scene, content, and interaction contracts.
- **Vite** — development server and production build.
- **Three.js** — real-time 3D renderer.
- **React Three Fiber** — React integration for Three.js scene composition.
- **React Three Drei** — useful helpers where appropriate.
- **GSAP or one equivalent animation library** — camera paths and deliberate timeline transitions.
- **CSS / CSS Modules / existing styling system** — DOM overlay UI.
- **Zustand or a small React context/reducer** — global experience state. Select one; do not introduce multiple competing stores.
- **MediaPipe Tasks Vision or another actively maintained, compatible face-landmark solution** — optional on-device face tracking for the selfie finale. Verify browser and device support before committing to a library.
- **Vitest and React Testing Library** — state, content, and UI tests where the repository supports them.
- **Playwright** — end-to-end journey tests where practical.

Do not install every listed option automatically. Inspect the repository, choose the smallest coherent stack, and explain any deviation.

### 2.2 Rendering architecture

The application should have:
1. A full-viewport 3D canvas.
2. A React DOM overlay above the canvas for chapter labels, progress, buttons, modals, copy, and accessibility.
3. A single experience state model controlling which scene/chamber and reveal state is active.
4. A shared camera rig that moves between authored waypoints.
5. Lazy-loaded scene assets, with the next destination prepared before the transition when practical.

The 3D scene must be built from actual Three.js objects, GLB/GLTF models, materials, lights, and scene geometry. A static background image with a CSS zoom effect is not an acceptable final replacement for a 3D environment.

### 2.3 Browser constraints

- The main experience must run in a modern WebGL-capable browser.
- Audio must follow browser autoplay restrictions.
- Camera access requires HTTPS in production (localhost is generally permitted for development) and explicit user permission.
- Camera access must be requested only when the visitor chooses the selfie feature.
- Provide fallback states for unsupported WebGL, failed assets, missing camera, denied camera permission, and unavailable audio.

---

## 3. High-level system architecture

```text
Browser
└── AppShell
    ├── ExperienceStore
    │   ├── CurrentChapter (01–05)
    │   ├── CurrentChamber (I–XII)
    │   ├── RevealState
    │   ├── ModalState
    │   ├── AudioState
    │   └── VisitorPreferences
    │
    ├── ExperienceViewport
    │   ├── ThreeCanvas
    │   │   ├── SharedLighting / Environment
    │   │   ├── CameraRig
    │   │   ├── ArrivalScene
    │   │   ├── EntranceScene
    │   │   ├── WelcomeHallScene
    │   │   ├── RoyalGalleryScene
    │   │   ├── MemorySalonScene
    │   │   ├── RoyalChamberScene
    │   │   ├── MessageHallScene
    │   │   ├── PalaceGardenScene
    │   │   ├── GiftReliquaryScene
    │   │   ├── CrownRoomScene
    │   │   ├── PortraitScene
    │   │   └── FinaleScene
    │   │
    │   └── ExperienceOverlay
    │       ├── ChapterHeader
    │       ├── FiveChapterProgress
    │       ├── BackControl
    │       ├── SoundToggle
    │       ├── PrimaryActions
    │       ├── ImperialNavigator (desktop/optional)
    │       ├── MemoryModal
    │       ├── GiftLedgerPanel
    │       ├── CrownInspectionModal
    │       ├── InvitationEnvelopeModal
    │       ├── SelfieCameraOverlay
    │       └── GuestbookPanel
    │
    ├── ContentRepository
    │   ├── InvitationContent
    │   ├── GalleryRecords
    │   ├── ChamberCopy
    │   └── AssetManifest
    │
    ├── AudioController
    ├── CameraPermissionController
    └── Diagnostics / ErrorBoundary
```

### 3.1 Responsibilities

| Module | Responsibility | Must not do |
|---|---|---|
| `AppShell` | Mount app, load config, provide global providers, handle fallbacks | Contain detailed 3D mesh logic |
| `ExperienceStore` | Hold chapter, chamber, sub-state, modal, and preference state | Directly manipulate Three.js objects |
| `ExperienceViewport` | Own the full-screen canvas and overlay composition | Duplicate business/content data |
| `CameraRig` | Execute camera paths, look-at targets, transitions, bounds | Own chapter content or UI copy |
| `Scene` modules | Build each chamber's geometry, lights, props, and interaction targets | Navigate by editing the DOM |
| `ExperienceOverlay` | Render accessible DOM controls and labels | Simulate 3D movement with CSS |
| `ContentRepository` | Load typed personal content and asset metadata | Hard-code content inside scene components |
| `AudioController` | Load, play, pause, and mute supplied audio | Claim sound is active if no audio is playing |
| `CameraPermissionController` | Request camera, track face landmarks, dispose camera streams | Upload or retain images without consent |
| `Diagnostics` | Capture errors and loading states | Expose sensitive camera frames or personal data |

---

## 4. Suggested repository layout

Adapt to the repository if it already uses another convention. Do not move or rename functioning project files just to match this example.

```text
royal-palace/
├── DESIGN.md
├── ARCHITECTURE.md
├── README.md
├── package.json
├── public/
│   ├── assets/
│   │   ├── models/
│   │   │   ├── palace/
│   │   │   ├── furniture/
│   │   │   ├── garden/
│   │   │   ├── envelope/
│   │   │   ├── crown/
│   │   │   └── crest/
│   │   ├── textures/
│   │   │   ├── architecture/
│   │   │   ├── floors/
│   │   │   ├── fabrics/
│   │   │   └── foliage/
│   │   ├── photographs/
│   │   ├── portraits/
│   │   ├── audio/
│   │   └── icons/
│   └── favicon.svg
├── src/
│   ├── app/
│   │   ├── App.tsx
│   │   ├── AppProviders.tsx
│   │   ├── ExperienceStore.ts
│   │   ├── experienceReducer.ts
│   │   ├── experienceTypes.ts
│   │   └── config.ts
│   ├── content/
│   │   ├── invitationContent.ts
│   │   ├── chamberContent.ts
│   │   ├── galleryRecords.ts
│   │   └── assetManifest.ts
│   ├── experience/
│   │   ├── ExperienceViewport.tsx
│   │   ├── ExperienceCanvas.tsx
│   │   ├── ExperienceOverlay.tsx
│   │   ├── ExperienceCoordinator.ts
│   │   └── LoadingFallback.tsx
│   ├── camera/
│   │   ├── CameraRig.tsx
│   │   ├── cameraWaypoints.ts
│   │   ├── cameraTimelines.ts
│   │   └── cameraCollision.ts
│   ├── scenes/
│   │   ├── shared/
│   │   │   ├── materials.ts
│   │   │   ├── lighting.ts
│   │   │   ├── architecture/
│   │   │   ├── props/
│   │   │   └── interaction/
│   │   ├── arrival/
│   │   │   └── ArrivalScene.tsx
│   │   ├── entrance/
│   │   │   └── EntranceScene.tsx
│   │   ├── welcome-hall/
│   │   │   └── WelcomeHallScene.tsx
│   │   ├── gallery/
│   │   │   └── RoyalGalleryScene.tsx
│   │   ├── memories/
│   │   │   └── MemorySalonScene.tsx
│   │   ├── royal-chamber/
│   │   │   └── RoyalChamberScene.tsx
│   │   ├── message-hall/
│   │   │   └── MessageHallScene.tsx
│   │   ├── gardens/
│   │   │   └── PalaceGardenScene.tsx
│   │   ├── reliquary/
│   │   │   └── GiftReliquaryScene.tsx
│   │   ├── crown/
│   │   │   └── CrownRoomScene.tsx
│   │   ├── portrait/
│   │   │   └── PortraitScene.tsx
│   │   └── finale/
│   │       └── FinaleScene.tsx
│   ├── interactions/
│   │   ├── interactionTypes.ts
│   │   ├── useScenePointer.ts
│   │   ├── DoorInteraction.ts
│   │   ├── PhotoFrameInteraction.ts
│   │   ├── EnvelopeInteraction.ts
│   │   └── CrownInteraction.ts
│   ├── overlays/
│   │   ├── ChapterHeader.tsx
│   │   ├── FiveChapterProgress.tsx
│   │   ├── ImperialNavigator.tsx
│   │   ├── SoundToggle.tsx
│   │   ├── MemoryModal.tsx
│   │   ├── GiftLedgerPanel.tsx
│   │   ├── CrownInspectionModal.tsx
│   │   ├── InvitationModal.tsx
│   │   ├── SelfieCameraOverlay.tsx
│   │   └── GuestbookPanel.tsx
│   ├── services/
│   │   ├── audio/
│   │   │   └── AudioController.ts
│   │   ├── camera/
│   │   │   ├── CameraPermission.ts
│   │   │   ├── FaceTracker.ts
│   │   │   └── PortraitCapture.ts
│   │   └── assets/
│   │       └── AssetLoader.ts
│   ├── styles/
│   │   ├── tokens.css
│   │   ├── global.css
│   │   └── overlay.css
│   └── test/
│       ├── experienceState.test.ts
│       ├── contentValidation.test.ts
│       └── navigation.test.ts
└── e2e/
    └── invitationJourney.spec.ts
```

The exact directory tree is advisory. The separation of concerns is mandatory; the exact filenames are not.

---

## 5. Experience state and navigation model

### 5.1 State model

Use explicit, typed state. Avoid scattered booleans such as `isGallery`, `isCrown`, `isModalOpen`, and `isFinal` that can create impossible combinations.

Recommended conceptual TypeScript types:

```ts
export type ChapterId =
  | "arrival"
  | "grand-entrance"
  | "royal-gallery"
  | "grand-ballroom"
  | "rose-garden";

export type ChamberId =
  | "chamber-1"
  | "chamber-2"
  | "chamber-3"
  | "chamber-4"
  | "chamber-5"
  | "chamber-6"
  | "chamber-7"
  | "chamber-8"
  | "chamber-9"
  | "chamber-10"
  | "chamber-11"
  | "chamber-12";

export type FinalRevealState =
  | "none"
  | "approaching-envelope"
  | "envelope-open"
  | "gift-ledger-open"
  | "crown-reveal"
  | "crown-inspection"
  | "portrait"
  | "selfie-camera"
  | "finale";

export type ModalState =
  | { type: "none" }
  | { type: "memory"; recordId: string }
  | { type: "invitation" }
  | { type: "crown-inspection" };

export interface ExperienceState {
  chapter: ChapterId;
  chamber: ChamberId;
  reveal: FinalRevealState;
  modal: ModalState;
  isTransitioning: boolean;
  audioEnabled: boolean;
  navigatorOpen: boolean;
  reducedMotion: boolean;
}
```

Use a reducer/store with named actions, for example:
- `START_EXPERIENCE`
- `SKIP_INTRO`
- `MOVE_TO_CHAMBER`
- `TRANSITION_STARTED`
- `TRANSITION_COMPLETED`
- `OPEN_MEMORY`
- `CLOSE_MEMORY`
- `OPEN_GIFT_LEDGER`
- `CLOSE_GIFT_LEDGER`
- `OPEN_ENVELOPE`
- `SHOW_CROWN`
- `OPEN_CROWN_INSPECTION`
- `CLOSE_CROWN_INSPECTION`
- `OPEN_SELFIE_CAMERA`
- `CLOSE_SELFIE_CAMERA`
- `SHOW_PORTRAIT`
- `SHOW_FINALE`
- `TOGGLE_AUDIO`
- `TOGGLE_NAVIGATOR`

### 5.2 Valid transition graph

```text
CHAPTER 01: ARRIVAL
  Chamber I — Grand Facade
      |
      | APPROACH THE PALACE
      v
CHAPTER 02: THE GRAND ENTRANCE
  Chamber II — Portal / Entrance
      |
      v
  Chamber III — Welcome Hall / Rotunda
      |
      v
CHAPTER 03: THE ROYAL GALLERY
  Chamber IV — Museum Gallery
      |
      v
  Chamber V — Memory Exhibition
      |
      v
CHAPTER 04: THE GRAND BALLROOM
  Chamber VI — Royal Chamber / Salon
      |
      v
  Chamber VII — Message Exhibition
      |
      v
CHAPTER 05: THE ROSE GARDEN
  Chamber VIII — Palace Gardens
      |
      v
  Chamber IX — Gift Exhibition / Reliquary
      |
      +----> Inspect Gift Ledger (open / close)
      |
      v
  Invitation Envelope (approach / open / read)
      |
      v
  Chamber X — Crown Room
      |
      +----> Crown Inspection Modal (open / close)
      |
      v
  Chamber XI — Final Royal Portrait
      |
      +----> Optional Selfie / Crown Camera
      |
      v
  Chamber XII — Imperial Finale
      |
      +----> Sign Guestbook
      +----> Return to Grand Facade
      +----> Revisit Crown
```

The gift/reliquary and envelope can be coordinated in one final-chapter sequence. Do not let a prototype's gift-casket text replace the personal envelope that is shown in the video. If the gift casket is retained as an additional exhibit, the personal invitation envelope remains a distinct interaction and must still be available.

### 5.3 Navigation rules

- Chapter progression is sequential by default.
- The user can use back navigation to revisit the previous meaningful chamber.
- The desktop Imperial Navigator may jump to an already available chamber, but should not interrupt an active transition.
- On mobile, keep the primary journey simple and linear; make the navigator a discreet optional panel.
- All scene-changing inputs are debounced/guarded while a transition is in progress.
- Closing a modal restores the exact camera/chamber state that was underneath it.
- A visitor must never be trapped in a modal, camera view, or animated state.
- `SKIP INTRO` skips camera movement, not the invitation text or the experience content.
- Camera animations may be skipped where necessary for accessibility or usability.
- Refreshing should start at the Arrival screen by default unless session persistence is intentionally implemented.

---

## 6. Detailed chamber architecture

Each chamber is a distinct 3D environment, but all environments share materials, proportions, lighting language, and the same visitor camera.

### Chamber I — The Grand Facade

**Chapter:** 01 — The Arrival  
**Purpose:** Establish the world and present the invitation.

**Environment:**
- Symmetrical European palace façade.
- Repeated windows across left and right wings.
- Distinct central pavilion/roof mass and main entrance.
- Warmly glowing windows.
- Formal symmetrical garden.
- Straight central pathway from foreground to the front entrance.
- Clipped hedges, formal beds, restrained topiary.
- Peach/apricot/rose/mauve sunset.
- Simplified low-poly architectural geometry.

**Composition:**
- Vertical 9:16 first.
- Palace dominates the upper/middle composition.
- Pathway provides a strong foreground-to-centre leading line.
- Keep the title and CTA legible against the environment.
- Do not cover the palace's central entrance with the name.

**Overlay copy:**
- `THE ARRIVAL · 01 / 05`
- `AN INVITATION`
- `Her Royal Highness`
- `Princess Gahana Ray`
- `A special evening awaits.`
- `APPROACH THE PALACE`
- `SKIP INTRO`

All copy is editable in the content layer.

**Camera:** Stable establishing view, subtle forward push; CTA advances to Chamber II.

### Chamber II — The Grand Royal Entrance / Portal

**Chapter:** 02 — The Grand Entrance  
**Purpose:** Cross the palace threshold.

**Environment and objects:**
- Monumental carved walnut double doors.
- Gold or antique-gold decorative relief/handles.
- Classical columns around the portal; Corinthian-inspired fluting may be used but should remain stylised.
- Symmetrical wall lanterns.
- Crest above the entrance if a supplied crest asset exists.
- Large pale stone entrance structure.
- Warm interior glow behind the doors.

**Interaction:**
- `CROSS THE THRESHOLD` / equivalent primary action.
- Door leaves rotate inward around correct pivots.
- The camera advances only once both doors have opened enough to clear the path.
- Show a temporary unlatched/opening state if desired.
- Continue into Chamber III.

**Important:** The Stitch HTML uses an “18ft” door description and a date-like architectural label. Those are content copy, not verified measurements/history. Store them as editable display copy only or omit them.

### Chamber III — The Grand Welcome Hall / Central Rotunda

**Chapter:** 02 — The Grand Entrance  
**Purpose:** Reveal the interior scale and the main staircase.

**Environment:**
- Large symmetrical rotunda/reception hall.
- Wide central staircase or bifurcated/twin-flight arrangement, consistent with the selected reference asset.
- Burgundy runner along the stairs.
- Pale marble/stone steps and landings.
- Tall columns and balustrades.
- Large chandelier at the centre.
- Ceiling medallion or dome detail.
- Tall arched windows.
- Checkered pale and dark stone floor in the foreground.
- Burgundy arched doorway at the upper landing.

**Content/UI from Stitch prototype:**
- Chamber identification.
- Welcome inscription plaque.
- Optional waypoint label indicating the direction to the Royal Galleries.

The long inscription in the HTML is sample copy. Keep it editable and do not make it a permanent unchangeable statement.

**Camera:** Enter from portal, hold the symmetrical staircase view, tilt slightly up to reveal the chandelier, return to eye level, then move towards the gallery exit.

### Chamber IV — The Royal Museum Gallery / Monumental Enfilade

**Chapter:** 03 — The Royal Gallery  
**Purpose:** Establish the long corridor where visitors discover the archive spaces.

**Environment:**
- Long, one-point-perspective gallery corridor.
- Repeating arched/curved ceiling bays.
- Chandeliers placed along the centre line.
- Burgundy wall panels with cream architectural borders.
- Tall arched windows.
- Central burgundy carpet runner.
- Warm wood/parquet floor or the reference's pale floor treatment; select one consistent material scheme per scene.
- Decorative columns/pilasters and alcoves.
- Clear double-door/corridor terminus at the far end.

**Side exhibition concepts from Stitch HTML:**
- West alcove: `The Queen's Drawing Collection`.
- East alcove: `The Coronation Vestments`.
- Small accession/provenance labels.

These are content slots, not mandatory factual historical exhibits. Keep the text editable and only show actual supplied assets/approved copy.

**Camera:** Slow forward corridor movement on the centre line. Slight optional camera glance to a selected frame/alcove. Do not turn the corridor into a grid of cards.

### Chamber V — The Memory Exhibition / Portrait & Archival Salon

**Chapter:** 03 — The Royal Gallery  
**Purpose:** Present the real personal photographs and memories.

**Environment:**
- Burgundy/damask-inspired wall treatment.
- Gilded or warm wood frames.
- Consistent portrait/frame sizes with restrained ornamental details.
- Soft focused exhibition lighting.
- Small engraved plaque beneath or above each frame.
- Gallery spacing that allows the visitor to focus on one photograph at a time.

**Three sample record concepts in the HTML prototype:**
1. `Her Highness at the Summer Solstice Ball` — archive reference `188-A`.
2. `The Imperial Rose Garden Dedication` — archive reference `204-C`.
3. `The Sovereign State Banquet` — archive reference `312-F`.

Use these as editable development examples only. Replace them with the owner's real images, titles, and notes. Never fabricate personal memories or substitute synthetic photographs of real people.

**Memory interaction:**
- Raycast/pointer/tap target on a physical photo frame.
- Open the Memory Inspection Modal with selected photograph, title, archive reference, and description.
- Modal has close and return actions.
- Closing the modal restores the camera to its pre-modal position.
- Mobile interaction must use tap; hover is only an optional desktop affordance.

### Chamber VI — The Grand Royal Chamber / Private Sovereign Salon

**Chapter:** 04 — The Grand Ballroom (chapter grouping label retained from the video)  
**Purpose:** A more intimate room before the proclamation/message space.

**Environment described in the Stitch prototype:**
- Hand-carved walnut-style wall panelling/boiserie.
- Antique-gold trim.
- Deep crimson/burgundy upholstery and wall details.
- Fireplace/hearth as a possible focal feature.
- Tall French/arched windows.
- Velvet chaise or selected royal furniture.
- Warm interior lighting.
- Restrained decorative elements.

**Curatorial detail cards in the HTML:**
- Hearth Relic / Carrara hearth detail.
- Brocade Weave / Lyon velvet detail.

Preserve the information layout as optional chamber overlays or inspection points. Treat dates, provenance and material claims as fictional/demo text unless owner-approved.

**Camera:** Enter with a slow forward move, glance towards the fireplace or main furniture, then move towards Chamber VII.

### Chamber VII — The Royal Message Exhibition / Imperial Proclamation Hall

**Chapter:** 04 — The Grand Ballroom  
**Purpose:** Present the main personalised dedication/message in a ceremonial way.

**Environment:**
- A clear central burgundy message stele/plaque.
- Antique-gold frame/trim.
- Crest or royal seal above the inscription if available.
- Symmetrical secondary forms/pedestals, such as busts or decorative stands.
- Warm controlled lighting.
- Clear negative space around the message.
- The room should be visually ceremonial but not crowded.

**Default prototype content structure:**
- `SOVEREIGN TESTAMENT • DECREE ROYAL`
- `An Ode to Her Royal Highness`
- Main dedication paragraph.
- Secondary dedication paragraph.
- Closing line.
- Seal of Registry / Heritage Custodian / Decree Status fields.

All these strings are editable. Do not lock the prose into the 3D model texture; render the long message as accessible DOM text on a plaque overlay or as readable text geometry only where it remains legible.

**Camera:** Approach, pause, focus the message, then continue into the garden.

### Chamber VIII — The Royal Palace Gardens / Formal Parterre

**Chapter:** 05 — The Rose Garden  
**Purpose:** Deliver the open outdoor reveal and calm emotional shift.

**Environment:**
- Formal, strongly symmetrical garden.
- Pale central walkway.
- Clipped green hedges forming geometric parterres.
- Red and pink rose beds.
- Rounded topiary trees and conical accents.
- Planters/pedestals positioned symmetrically.
- Circular fountain/basin on the centre axis.
- White domed gazebo/pavilion beyond the fountain.
- Distant palace façade visible behind the garden.
- Peach/pink/golden twilight sky.

**Three garden information concepts from Stitch HTML:**
- `The Latona Basin` — fountain/water detail.
- `The Sovereign Arabesques` — hedge/parterre geometry.
- `Golden Twilight Aspect` — garden lighting/time-of-day note.

These may appear as small optional inspection labels or restrained information panels. Do not cover the scene with a row of standard web cards.

**Default garden line:** `Every rose here is yours.`

**Camera:** Begin on the centre path, approach the fountain/gazebo, pan gently to the roses, then continue to the gift/envelope display.

### Chamber IX — The Royal Gift Exhibition / Sovereign Reliquary

**Chapter:** 05 — The Rose Garden  
**Purpose:** Provide the pedestal-based gift/invitation interaction.

**Visual reference from HTML:**
- Circular pale marble pedestal/plinth.
- Fluted/rounded pedestal base.
- Warm spotlight.
- Decorative display object/casket may use walnut, velvet, antique-gold filigree, pearls, ribbon, and wax-seal motifs.
- Small record/provenance information.
- An `INSPECT RELIQUARY LEDGER` control that expands/collapses the object's detail note.

**Critical source reconciliation:** The original video shows a personal envelope on a pale pedestal in the garden. The HTML prototype describes a gift casket. Preserve the Chamber IX reliquary concept, but the **personal envelope and invitation reveal must remain a distinct, required interaction**. Do not replace the envelope with an unrelated casket. The casket can be an optional accompanying artefact if the owner wants both.

**Interaction:**
- Approach the pedestal.
- Inspect/expand the gift ledger if this feature is retained.
- Activate `OPEN THE ENVELOPE` to reveal the personal invitation.
- Envelope opening should be a deliberate object animation, not a page jump.

### Chamber X — The Grand Royal Crown Room

**Chapter:** 05 — The Rose Garden  
**Purpose:** Crown reveal and optional inspection.

**Environment from HTML:**
- Grand crown chamber/rotunda concept.
- Large central crown display.
- Pale marble pedestal.
- Crimson/burgundy velvet cushion.
- Warm spotlight and restrained jewel glints.
- Optional architectural columns/rotunda framing.

**Crown visual source reconciliation:**
- The original video screenshot shows a delicate silver/diamond tiara on a burgundy cushion.
- The HTML text describes a more elaborate gold imperial crown with rubies, emeralds, pearls, and a large gem ledger.
- The video-reference tiara is the default visual asset for the reveal and selfie overlay.
- If the owner explicitly approves the gold Imperial Crown from the HTML as a separate second artefact, it can be offered in the inspection modal. Do not silently substitute the gold crown for the silver tiara that appears in the supplied video.

**Crown interaction:**
- Slow camera approach.
- A restrained 15–20 degree orbit or controlled close inspection, not an uncontrolled spin.
- Subtle gemstone highlights/sparkle.
- `INSPECT JEWELS` opens the Crown Inspection Modal.
- Modal contains a close-up image/model, editable provenance copy, and configurable gemstone information.
- The close action restores the visitor to the crown chamber.

**Important:** The HTML labels an image pane “360 Axis Live View”. Do not claim it is a real 360 view if it is only a static image. A true 360 inspection requires a rotatable 3D crown model or a set of multi-angle views.

**Gemstone numbers and historical statements** appearing in the HTML (for example, diamond totals, carat weights, named stone origins, provenance, vault/security claims) are demo copy only. Do not publish them as real facts unless the owner provides/approves them.

### Chamber XI — The Final Royal Portrait

**Chapter:** 05 — The Rose Garden  
**Purpose:** Present the final official portrait/keepsake moment.

**Environment:**
- Large portrait inside a monumental antique-gold frame.
- Burgundy/velvet surround.
- Soft gallery lighting.
- Clear official title plaque below or over the lower part of the portrait.
- The portrait should feel like a museum masterpiece and visually close the crown/portrait sequence.

**Portrait requirements:**
- Use an owner-supplied portrait or a visitor-created portrait with consent.
- Do not fabricate a likeness of Princess Gahana or another real person.
- Keep portrait title and description editable.
- The HTML's canvas dimensions and “commissioned” narrative are placeholders unless approved.

**Selfie option:** The camera/tiara feature from the original video may be offered as an alternate way to create the final portrait. It must remain optional and should use the same tiara asset as Chamber X.

### Chamber XII — The Final Palace Experience / Imperial Finale

**Chapter:** 05 — The Rose Garden  
**Purpose:** Emotional closure, completion, and optional guestbook action.

**Environment:**
- Palace silhouette at deep twilight/night.
- Warm glowing windows.
- Dark, calm backdrop with restrained star/ambient detail.
- Crest/seal centred above final message.
- Burgundy/dark walnut surfaces and antique-gold highlights.

**Content structure from HTML:**
- `An Eternal Sovereign Legacy`
- Closing dedication/quotation.
- Completion message.
- Guestbook name/note field.
- `Inscribe Seal` action.
- Return to Grand Facade.
- Revisit Crown Jewels.

All long copy remains owner-editable.

**Guestbook behaviour:**
- Validate that the input is not empty.
- Show an in-session confirmation after submission.
- Do not imply the note is permanently stored if there is no backend/persistence.
- If persistent guestbook storage is later implemented, disclose what is stored and provide appropriate consent/security controls.
- Do not send the visitor's note to any server by default.

---

## 7. UI architecture and visual overlay

### 7.1 Overlay/canvas separation

The 3D scene renders underneath. UI elements should be rendered in DOM above the canvas for legibility, accessibility, touch handling, and text selection.

Do not bake long paragraphs into textures. Use 3D text only for short architectural labels where it improves the scene; render invitation/message body copy as DOM overlays or an accessible modal.

### 7.2 Persistent top header

The mobile-first header follows the reference:
- Back arrow where applicable.
- Chapter title.
- Chapter counter `01 / 05` through `05 / 05`.
- Small progress line/marks.
- Sound toggle in the top-right.

Examples:
- `THE ARRIVAL · 01 / 05`
- `THE GRAND ENTRANCE · 02 / 05`
- `THE ROYAL GALLERY · 03 / 05`
- `THE GRAND BALLROOM · 04 / 05`
- `THE ROSE GARDEN · 05 / 05`

### 7.3 Nine blue eye-shaped symbols (removed)

**Removed by owner instruction (2026-11-20).** The row of nine blue eye symbols (🧿) seen in the reference screenshots is an emoji overlay added when the video was edited, like the Instagram watermark. It is not part of the product: do not implement it. The five-dash chapter progress beneath the chapter label remains.

### 7.4 Imperial Navigator from Stitch HTML

The HTML includes a floating desktop-side panel:
- `Imperial Navigator`
- Active Roman chamber number/name
- Twelve quick waypoints I–XII
- `Palace Resonance` audio control

Preserve its function as secondary navigation:
- Desktop: compact floating side navigator, shown only when there is sufficient width.
- Mobile: collapsed into a discreet button/drawer or omitted from the main scene in favour of the five-chapter top progress.
- The active chapter/chamber values are derived from application state, not DOM scroll position.
- It should not create a visible traditional webpage sidebar during the main mobile journey.

### 7.5 Site identity/header concept in HTML

The HTML includes:
- Royal crest.
- `The Royal Palace`
- Subtitle: `An Interactive Digital Museum & Heritage Exhibition`
- Overview / Archives / Chronology / Visitor Guide links.
- Profile icon.

Do not let this become a fixed conventional website header that competes with the first-person scene. If retained, use it as a discreet desktop entry/overview shell or an optional museum information panel. The primary immersive experience should still occupy the screen.

### 7.6 Theme tokens

Use the existing Palatial Heritage tokens from `DESIGN.md` as the base for interface and typography.

| Token / purpose | Value |
|---|---|
| Main dark surface | `#1F0F0A` |
| Antique gold primary | `#E9C178` |
| Antique gold container | `#C6A15B` |
| Champagne/tertiary | `#D7C596` |
| Deep burgundy accent | `#45151F` |
| Dark walnut | `#35221C` |
| Warm ivory scene/UI text | `#F4EBDD` |
| Secondary rose | `#FFB2BC` |
| Muted text | `#D1C5B4` |
| Hairline outline | `#9A8F80` |

For the 3D architecture use the scene palette defined in `DESIGN.md`: warm cream/beige stone, taupe shadows, burgundy carpet/walls, muted antique gold, dark green hedges, rose accents, and sunset tones. The interface can remain darker than the 3D world.

### 7.7 Typography

- Playfair Display: main names, section/chamber headings, royal labels.
- Newsreader: narrative copy, messages, archival descriptions.
- A restrained sans-serif: compact UI labels and controls.
- Keep the princess's name large, clear, and elegant.
- Use uppercase, letter-spaced small labels for chapter navigation.
- All text must remain editable and responsive.
- Fonts should be locally bundled or have reliable fallbacks; do not make successful rendering depend on a remote font request.

### 7.8 Modal/panel components

The Stitch prototype has two main modal patterns and several expandable areas. Implement them as React components controlled by state:

1. **Memory Inspection Modal** — selected photograph, record number, title, image, description, return/close.
2. **Crown Inspection Modal** — crown close-up/3D model, gem details, provenance text, close.
3. **Gift Ledger Panel** — expandable/collapsible curatorial details.
4. **Invitation Envelope Modal** — opened invitation and event details.
5. **Selfie Camera Overlay** — live camera preview, face/tiara overlay, capture, retake, close.
6. **Guestbook Confirmation** — in-session success state.

Each modal/panel must:
- Have a clear close action.
- Trap focus appropriately while open.
- Close with Escape where appropriate.
- Return to the scene without resetting camera state.
- Work on touch and keyboard.
- Avoid stacking multiple unrelated modals at once.

---

## 8. Camera rig and movement architecture

### 8.1 First-person point of view

- No visible character/avatar.
- Camera represents visitor eye position.
- Target standing height: approximately 1.55–1.70 world units (calibrate to asset scale).
- Use a perspective camera with a mobile-friendly field of view. Start around 45–55 degrees and adjust after visual comparison; do not fix a value without testing.
- Keep the camera's roll level except for very subtle stylised effects if specifically needed.
- The camera should not feel like a drone or a security camera.

### 8.2 Camera movement modes

The `CameraRig` should support:
- `ESTABLISHING` — stable scene introduction.
- `DOLLY_FORWARD` — slow forward approach.
- `LOOK_AT` — controlled pan/tilt to a target.
- `PATH_FOLLOW` — follow authored path through corridor/garden.
- `ORBIT_TARGET` — small controlled orbit around crown or another inspection object.
- `PAUSE` — hold a framing while visitor reads.
- `USER_LOOK` — optional limited pointer/touch look.
- `RETURN_TO_WAYPOINT` — return to a saved view after an inspection modal.
- `SKIP_TO_END` — jump to the end pose for a skippable cinematic sequence.

### 8.3 Movement design principles

- Camera paths should be authored as explicit waypoints/timelines, not improvised from arbitrary DOM scroll positions.
- Use smooth interpolation/easing.
- Keep moves short enough to avoid frustrating waits.
- A subtle walking bob may be used sparingly; do not create noticeable motion sickness.
- Avoid aggressive head bob, roll, acceleration, zoom snaps, or fast spins.
- Provide reduced-motion handling.
- Ensure the route avoids collisions with walls, door frames, steps, picture frames, garden objects, and pedestals.
- Use collision/bounds checks where interactive free movement is provided.
- When not using free movement, prefer authored cinematic paths so the visitor always sees the intended focal composition.

### 8.4 Camera waypoint data

Keep paths in configuration, separate from scene components. Each waypoint should define:
- Position `[x, y, z]`.
- Target/look-at point `[x, y, z]`.
- Duration.
- Easing.
- Optional scene event/callback.
- Optional skip target.
- Whether visitor input is temporarily locked.

Example shape:

```ts
export interface CameraWaypoint {
  id: string;
  position: [number, number, number];
  lookAt: [number, number, number];
  durationMs: number;
  easing: "power1.inOut" | "power2.inOut" | "sine.inOut" | "linear";
  lockInput?: boolean;
  onArrive?: string;
}
```

The exact easing string/type may be adjusted to the chosen animation library.

### 8.5 Camera choreography by chamber

| Chamber | Start framing | Main movement | End framing |
|---|---|---|---|
| I Facade | Central garden path facing palace | Gentle push toward main entrance | Palace entrance fills central axis |
| II Portal | Facing closed double doors | Door leaves open; camera crosses threshold | Interior is revealed |
| III Rotunda | Centre of hall facing staircase | Move towards stair/landing; tilt up to chandelier | Gallery exit in view |
| IV Gallery | Centre of corridor facing vanishing point | Forward path; subtle looks toward side frames | Far doors / Memory Salon |
| V Memories | Gallery/Salon viewpoint | Small moves toward selected photographs | Return to main gallery axis |
| VI Salon | Facing main interior feature | Slow reveal/pan across room | Message hall exit |
| VII Stele | Facing central inscription | Gentle dolly toward message | Readable plaque framing |
| VIII Garden | Start of central path | Move toward fountain/gazebo; subtle rose-bed glance | Gift display/pedestal |
| IX Reliquary | Facing marble pedestal | Approach and lower framing to object | Envelope/gift interaction point |
| X Crown | Crown/pedestal centred | Slow approach and limited orbit | Crown close-up |
| XI Portrait | Portrait framed frontally | Small push-in; settle on portrait | Final portrait composition |
| XII Finale | Palace silhouette/crest centred | Gentle final settle/fade | Dedication/guestbook in readable overlay |

---

## 9. 3D scene construction and asset system

### 9.1 General scene rules

- Use real 3D geometry for architecture, floors, walls, stairs, door leaves, hedges, fountain, pavilion, pedestal, envelope, and crown where appropriate.
- Use GLB/GLTF for complex hero assets if they are efficient and available.
- Use procedural geometry for repeated simple architecture (windows, columns, arch segments, hedge sections, balusters, planters) where it is more efficient and controllable.
- Reuse materials and geometries.
- Keep visual detail balanced with the low-poly reference style.
- Use texture detail selectively, not as a substitute for 3D form.
- Keep lighting attractive and performant on mobile.

### 9.2 Shared architectural components

Build reusable components where it reduces duplication:
- `WallSegment`
- `ArchedWindow`
- `Column`
- `Pilaster`
- `ArchSegment`
- `Cornice`
- `Balustrade`
- `StairFlight`
- `DoubleDoor`
- `Chandelier`
- `PictureFrame`
- `Pedestal`
- `Planter`
- `HedgeSegment`
- `Topiary`
- `RoseCluster`
- `Fountain`
- `Gazebo`
- `MessagePlaque`
- `CrownDisplay`

Component parameters should support colour, scale, material, and optional decorative detail. Do not create a huge generic architectural framework before one scene is working; build reusable components as real repetition becomes clear.

### 9.3 Materials

Centralise shared materials. Suggested material groups:
- `warmStone`
- `creamPlaster`
- `mutedGold`
- `darkWalnut`
- `burgundyVelvet`
- `parquetWood`
- `checkerStoneLight`
- `checkerStoneDark`
- `gardenHedge`
- `lawnOlive`
- `roseRed`
- `roseDustyPink`
- `marbleIvory`
- `crownSilver`
- `gemstoneDiamond`

Avoid excessive physically based material complexity. Use simple, stable materials where they match the reference.

### 9.4 Hero assets

Prioritise asset quality for:
1. Palace façade.
2. Main doors.
3. Chandeliers.
4. Personal photographs/frames.
5. Fountain and domed gazebo.
6. Envelope.
7. Silver diamond tiara.
8. Final portrait frame.

Hero assets should have correct pivots/origins for animation:
- Doors pivot at their hinges.
- Envelope flap has a separate pivot if animated.
- Crown/tiara pivot is at the centre of its base for controlled inspection.
- Chandelier pivot is at its suspension point if any motion is added.

### 9.5 Asset manifest

Maintain a manifest with:
- Asset key.
- File path.
- Asset type (`model`, `texture`, `image`, `audio`).
- Approximate size.
- Which scenes use it.
- Loading priority.
- Fallback asset.
- Whether it is owner-supplied, licensed, or placeholder.

No unlicensed or hot-linked remote assets should be relied upon for production. Download/locally bundle assets where usage rights allow and provide attribution/licence notes as required.

---

## 10. Personal content and data contracts

All user-specific information lives outside the scene code.

### 10.1 Invitation content

Conceptual configuration:

```ts
export interface InvitationContent {
  honoree: {
    honorific: string;
    displayName: string;
  };
  arrival: {
    eyebrow: string;
    supportingLine: string;
    primaryAction: string;
    secondaryAction: string;
  };
  ballroom: {
    message: string;
  };
  garden: {
    message: string;
  };
  event: {
    title?: string;
    date?: string;
    time?: string;
    venue?: string;
    address?: string;
    dressCode?: string;
    rsvp?: string;
    additionalMessage?: string;
  };
  finale: {
    heading: string;
    message: string;
  };
}
```

### 10.2 Memory record

```ts
export interface MemoryRecord {
  id: string;
  imageSrc: string;
  title: string;
  recordLabel?: string;
  caption?: string;
  description?: string;
  altText: string;
  imageFit?: "cover" | "contain";
  focusPosition?: string;
}
```

### 10.3 Chamber information record

```ts
export interface ChamberInfo {
  id: ChamberId;
  romanNumeral: string;
  title: string;
  chapterId: ChapterId;
  shortLabel: string;
  optionalDescription?: string;
}
```

### 10.4 Guestbook record

The prototype guestbook may initially be client-side only. If no backend exists:
- Validate the input.
- Show a confirmation for the current session.
- Do not say that a message has been permanently inscribed or saved.
- Do not create a fake persistence layer.

If a backend is later added, define data retention, consent, access controls, and deletion policy before storing guestbook entries.

---

## 11. Interaction architecture

### 11.1 3D interaction targets

3D click targets must map to typed actions. Avoid direct DOM lookup from Three.js scene code.

Examples:
- Entrance door → `CROSS_THRESHOLD`
- Photo frame → `OPEN_MEMORY(recordId)`
- Gift ledger exhibit → `TOGGLE_GIFT_LEDGER`
- Envelope → `OPEN_ENVELOPE`
- Crown → `OPEN_CROWN_INSPECTION`
- Portrait camera action → `OPEN_SELFIE_CAMERA`
- Final seal → `SIGN_GUESTBOOK`

### 11.2 Pointer and touch behaviour

- Use raycasting or React Three Fiber event handlers for scene objects.
- Provide visual feedback on hover/focus where applicable.
- Use tap/click as the primary interaction on mobile.
- Do not make the entire environment randomly clickable.
- Give interaction objects clear affordances (gentle highlight, plaque, button prompt, or focus cue).
- Prevent click-through to objects behind a modal.
- Guard double activation and rapid repeated interactions.
- Keep all interface controls accessible as DOM buttons.

### 11.3 Existing HTML prototype interactions to preserve

The source HTML contains these functional ideas:
- `scrollToChamber(...)` → replace with `navigateToChamber(...)` and the camera rig.
- `triggerDoorTransition()` → actual door hinge animation plus camera threshold traversal.
- `toggleGiftDetails()` → `GiftLedgerPanel` open/closed state.
- `openMemoryModal(...)` / `closeMemoryModal()` → selected `MemoryRecord` and modal state.
- `openCrownInspectionModal()` / `closeCrownModal()` → Crown Inspection Modal state.
- `signGuestbook()` → validated guestbook submission and truthful confirmation.
- `togglePalaceAudio()` → real audio controller state and playback if assets exist.
- `chamberMap` / active navigator → typed `ChamberInfo` map derived from state, not browser scroll position.

Do not retain the original inline global JavaScript functions or direct `document.getElementById` manipulation in the final React application.

---

## 12. Audio architecture

The Stitch HTML presents a `Palace Resonance` toggle. Preserve it as a functional sound control.

- The audio controller owns loading and playback.
- User interaction is required before playing sound.
- The button label/icon must represent the actual state.
- If no audio file is supplied, either hide/disable the control or show a truthful “Sound unavailable” state; do not simulate playback.
- Background ambience, if supplied, should be low-volume and non-intrusive.
- Optional effects can be used for doors, transitions, envelope opening, and crown reveal.
- Mute/disable should stop or pause playback appropriately.
- Stop/release audio resources when no longer needed.
- Respect reduced-motion and accessibility preferences; audio remains optional.

---

## 13. Camera/selfie and crown-overlay architecture

### 13.1 User journey

The selfie camera is an optional finale after the crown/portrait reveal:
1. Visitor selects a clear camera/portrait action.
2. Explain that the front-facing camera will be opened for the portrait effect.
3. Request permission.
4. Start the video stream only after permission is granted.
5. Run face landmark detection locally where feasible.
6. Position the silver/diamond tiara overlay above the forehead.
7. Smooth landmark motion to minimise jitter.
8. Allow capture, retake, close, and save/download if supported.
9. Stop all media tracks when the view closes or the experience ends.

### 13.2 Face tracking

Track at least:
- Face centre.
- Head scale/distance.
- Head rotation/yaw/roll if supported.
- Forehead/upper-face anchor.

Use a smoothed transform for the tiara:
- Position follows the forehead anchor.
- Scale is derived from face width.
- Rotation follows head roll.
- Small calibration offsets allow alignment.
- Keep the overlay stable under subtle head movement.

Do not rely on fixed screen coordinates. The overlay must follow the tracked face.

### 13.3 Failure states

Handle:
- Camera permission denied.
- No camera device.
- Camera already in use.
- Face not detected.
- Multiple faces.
- Tracking model failed to load.
- Browser does not support the chosen API.
- Visitor closes the camera during tracking.

Fallback:
- Offer a static portrait upload if the owner wants that workflow.
- Or let the visitor continue to the finale without taking a photo.
- If no face tracking is available, a simple aligned overlay may be offered as a labelled fallback, but do not claim it tracks the face.

### 13.4 Privacy

- No camera access on initial page load.
- No background recording.
- No image upload or storage by default.
- Stop the media stream immediately on close/unmount.
- If capture is local, keep it local unless the visitor explicitly chooses a supported download/share action.
- Explain clearly what happens to a captured photo.

---

## 14. Responsive layout strategy

### 14.1 Primary layout: portrait mobile

The visual reference is vertical. Prioritise 9:16 composition:
- Camera framing is authored for portrait first.
- Chapter title and chapter progress fit within the top safe area.
- The main scene occupies almost the entire viewport.
- The primary action is placed above the bottom safe area.
- Do not put a permanent full-width conventional navigation header over the scene.
- The photo, envelope, tiara, and plaque remain large enough to interact with.

### 14.2 Desktop and tablet

- Use adaptive camera framing and field of view.
- Avoid stretching a portrait scene to fill a wide screen.
- The twelve-chamber navigator may be available on desktop as a side panel.
- Do not show the desktop navigator as a mandatory mobile control.
- Ensure the 3D scene remains visually composed when wider; consider subtle environmental extension rather than excessive crop.

### 14.3 Device safe areas

Use `env(safe-area-inset-top)` and `env(safe-area-inset-bottom)` for fixed overlay controls where supported. Verify browser viewport behaviour on iOS Safari and Android Chrome.

---

## 15. Performance architecture

The project must work on current mid-range mobile devices, not just a high-powered development desktop.

### 15.1 Loading strategy

- Load the minimum assets needed for Chamber I first.
- Preload Chamber II while the visitor is in Chamber I where practical.
- Load later scenes progressively.
- Display a restrained loader during unavoidable load work.
- Avoid downloading all 12 chamber assets in one blocking request.
- Cache reusable models/textures appropriately.
- Provide a low-resolution or simplified fallback for large assets.

### 15.2 Rendering and scene optimisation

- Use a single WebGL renderer/canvas for the experience where practical.
- Avoid mounting all heavy scenes at once.
- Unmount or deactivate distant chambers when safe.
- Reuse geometries and materials.
- Use instancing for repeated hedges, roses, windows, columns, and balusters where appropriate.
- Limit real-time shadows and shadow-map sizes.
- Use baked lighting or simpler lighting for stable mobile performance.
- Limit post-processing; do not add bloom/DOF if it damages readability or frame rate.
- Use compressed textures and GLB/GLTF compression where supported.
- Dispose of scene resources when they are no longer referenced.
- Avoid unnecessary React re-renders in the render loop.
- Avoid layout reflows during camera animation.

### 15.3 Quality scaling

Create practical quality tiers based on device capability:
- High: higher shadow/detail settings for capable desktop/tablet.
- Balanced: default mobile setting.
- Low: reduced shadow resolution, simplified materials, fewer decorative particles, lower texture resolution.

Do not remove a story-critical asset or interaction when lowering quality.

### 15.4 Performance acceptance targets

Treat these as engineering targets to measure, not claims:
- Smooth interaction on a modern mid-range phone.
- Avoid persistent frame drops during camera movement.
- Keep initial load bounded by only the first scene and essential UI.
- No huge texture/model downloads without progressive loading.
- Stable memory when moving between all chambers.
- No runaway animation loops or leaked media streams.

---

## 16. Accessibility, safety, and robustness

- All UI controls must be semantic buttons/links.
- Interactive 3D objects must have an equivalent accessible control in the overlay or navigator.
- Support keyboard focus and activation.
- Use readable contrast and legible type.
- Respect `prefers-reduced-motion`.
- Provide a skip option for long animations.
- Provide a mute control.
- Do not make essential invitation details dependent only on sound or 3D movement.
- Use accessible text for personal message and event information.
- Use meaningful alt text for personal images.
- Camera permission is optional and user-initiated.
- Do not collect/store camera content or guestbook data silently.
- Keep personal photographs local to the application unless the owner explicitly chooses a remote host.
- Never expose API keys in client code.
- Use a clear error boundary and recoverable fallback view.

---

## 17. Failure and fallback strategy

| Failure | Expected behaviour |
|---|---|
| WebGL unavailable | Show a polished 2D fallback with invitation content and chapter navigation |
| Scene model fails | Show a simplified procedural replacement or neutral placeholder |
| Photo fails | Keep the frame, show a neutral fallback, and log the missing asset |
| Audio file missing | Disable/hide sound control honestly |
| Camera denied | Explain and allow the visitor to continue without selfie |
| Face tracker fails | Offer static portrait/fallback or skip |
| Transition interrupted | Resolve to a valid camera waypoint and valid state |
| Mobile device is slow | Reduce rendering quality, not chapter content |
| Refresh mid-journey | Start at Arrival cleanly unless session restoration has been deliberately implemented |

---

## 18. Testing strategy

### 18.1 Unit tests

Test:
- Five-chapter to twelve-chamber mapping.
- Valid/invalid state transitions.
- Modal open/close and return state.
- Gift ledger toggle.
- Memory record selection.
- Guestbook empty-input validation.
- Audio state consistency.
- Camera permission states.
- Content schema validation.
- Missing asset fallback.

### 18.2 Integration tests

Test:
- Arrival CTA starts the experience.
- Door button starts door animation once.
- Door animation completes and advances to Welcome Hall.
- Chamber IV navigation reaches Memory Exhibition.
- Photo frame opens correct memory.
- Modal closes to the same chamber/view.
- Message plaque opens or highlights the full message.
- Garden route reaches the gift/envelope pedestal.
- Envelope opens invitation content.
- Crown can be inspected and returned from.
- Portrait/selfie is optional.
- Finale guestbook shows truthful confirmation.
- Return-to-facade and revisit-crown actions work.

### 18.3 Visual QA

Compare the running app with supplied screenshots at the same portrait aspect ratio.

Specifically verify:
- Palace scale and symmetry.
- Sunset palette.
- Staircase composition, checkered floor, burgundy runner, chandelier.
- Gallery's long vaulted perspective, chandeliers, burgundy walls, frames, and runner.
- Ballroom parquet, chandelier, flowers, and plaque.
- Garden path, formal hedges, roses, fountain, gazebo, distant palace.
- Envelope/pedestal composition.
- Silver tiara on burgundy cushion.
- Top chapter label, five-dash progress, sound icon, and button placement.

### 18.4 Device QA

At minimum test:
- Desktop Chrome.
- Mobile Chrome or Android browser.
- iOS Safari if available.
- Portrait and landscape changes.
- Reduced-motion setting.
- Audio blocked/unavailable.
- Camera permission granted/denied.

---

## 19. Implementation milestones

Claude Code should implement in controlled milestones. Do not attempt to generate all 12 complex chambers in one giant untested change.

### Milestone 0 — Repository audit
- Inspect package scripts and existing framework.
- Inspect current code, assets, and Stitch export.
- Identify reusable design tokens and existing UI.
- Identify missing 3D models, photographs, audio, and content.
- Report the proposed implementation map.
- Do not overwrite working project files.

### Milestone 1 — Runtime foundation
- Set up app shell, canvas, error boundary, loading state.
- Create typed experience state.
- Create five-chapter/twelve-chamber mapping.
- Implement UI overlay, chapter header, progress motif, sound toggle, and optional navigator.
- Verify mobile viewport.

### Milestone 2 — First playable vertical slice
Build only:
- Chamber I exterior.
- Chamber II doors.
- Chamber III welcome hall.
- Shared camera rig and door transition.
- Basic mobile interaction.

This must look and feel close to the supplied reference before adding all other scenes.

### Milestone 3 — Royal Gallery
- Chamber IV corridor.
- Chamber V photo frames.
- Memory modal.
- Configurable personal photo records.
- Gallery camera path.

### Milestone 4 — Ballroom and message
- Chamber VI private salon.
- Chamber VII message hall/stele.
- Editable inscription content.
- Camera movement and message interaction.

### Milestone 5 — Garden and gift
- Chamber VIII garden.
- Fountain, hedges, flowers, gazebo.
- Chamber IX reliquary/pedestal.
- Gift ledger.
- Envelope object and invitation reveal.

### Milestone 6 — Crown and portrait
- Chamber X crown room.
- Tiara model/display.
- Crown inspection view/modal.
- Chamber XI official portrait.
- Optional live selfie/tiara overlay.

### Milestone 7 — Finale
- Chamber XII night/twilight finale.
- Closing dedication.
- Guestbook input/confirmation.
- Return-to-facade and revisit-crown controls.

### Milestone 8 — Polish and release
- Mobile performance tuning.
- Asset compression and progressive loading.
- Accessibility/reduced motion.
- Cross-browser and device testing.
- Production build.
- Update README with setup, content replacement, and deployment instructions.

After each milestone, Claude Code should summarise:
- What has been implemented.
- What is still a placeholder.
- Which owner-supplied assets/content are required.
- Build/test results.
- Any deviation from this architecture and why.

---

## 20. Important notes about the supplied Stitch HTML

The HTML export is a valuable visual/content prototype. It includes:
- A branded site header with royal crest and navigation links.
- A floating Imperial Navigator with Roman numeral chambers I–XII.
- `Palace Resonance` sound toggle.
- Twelve chamber sections.
- Memory Inspection Modal.
- Gift Ledger expand/collapse interaction.
- Crown Inspection Modal.
- Guestbook entry and confirmation.
- Return-to-facade and revisit-crown navigation.
- A chamber map and scroll-position-driven active navigator.

However, the HTML uses:
- Static CSS `background-image` environments.
- Normal page sections and `scrollIntoView`.
- Inline global JavaScript.
- DOM lookup and class manipulation.
- Simulated audio state rather than actual audio playback.
- A static image labelled as a 360 crown view.

These are prototype mechanisms, not the final architecture. Translate their **content, scene order, labels, visual ideas, and interaction intent** into React state and actual 3D scenes.

Do not copy the static background-image approach as the final environment renderer. Do not keep inline global functions or direct DOM class mutation in the React implementation. Do not call a static crown image a 360-degree viewer.

### Prototype content that must remain editable

The HTML contains elaborate fictional curatorial text and precise-looking values, including architectural dates/measurements, accession codes, material/provenance descriptions, crown gemstone quantities and weights, security claims, canvas dimensions, and registry statements. Treat all such values as editable illustrative content. Do not publish them as factual or historical claims without owner approval.

---

## 21. Definition of done

The application is complete only when:

- It is a working browser-based 3D experience, not merely a visual mockup.
- All five primary chapters and all twelve named chambers are represented.
- The first-person camera travels through connected environments.
- The visual style matches the supplied stylised low-poly reference.
- The five-chapter top progress treatment is preserved (eye symbols removed by owner instruction, §7.3).
- The optional twelve-chamber navigator works without dominating mobile.
- All personal photographs are owner-provided and interactive.
- Memory Inspection Modal works.
- Private Salon and Message Exhibition content is present and editable.
- Garden, fountain, hedges, roses, and gazebo are present.
- Gift/reliquary inspection works.
- The personal envelope and invitation reveal are present and distinct.
- The crown reveal and inspection work.
- The final portrait chamber and twilight finale work.
- The guestbook action is truthful about whether data is stored.
- The optional camera/tiara selfie works where supported and fails gracefully where unsupported.
- Audio control reflects actual playback.
- No scene transition leaves the app in an invalid state.
- The mobile experience is polished at 9:16.
- Performance, loading, accessibility, and fallback behaviours have been tested.
- The owner can replace text, photographs, event details, and key assets through documented configuration.

---

## 22. Final creative test

Before approving any implementation, compare it directly with the supplied reference video and screenshots.

Ask:

1. Does the arrival scene have the same centred palace, formal path, sunset, and invitation hierarchy?
2. Does the visitor feel like they are physically entering the palace?
3. Does the entrance hall preserve the staircase, checkered floor, burgundy runner, and chandelier?
4. Does the gallery have the long vaulted corridor, chandeliers, burgundy walls, frames, and central runner?
5. Does the ballroom preserve the parquet floor, symmetrical composition, chandelier, flowers, and central plaque?
6. Does the Rose Garden preserve the central path, hedges, roses, fountain, gazebo, and palace backdrop?
7. Are the personal photographs, messages, gift/envelope, crown, portrait, and finale still present?
8. Does the silver/diamond tiara from the video remain the default selfie crown?
9. Is the five-chapter progression clear, with all twelve chambers retained as the deeper content structure?
10. Does the result feel like one continuous royal invitation world instead of unrelated pages?

If a proposed implementation makes the experience more like a conventional website, removes an important chamber, changes the visual style, or loses the first-person movement, it is a regression. Rework it to match this architecture.

**Final product statement:** The finished experience should feel like stepping into a beautifully stylised royal invitation made especially for Princess Gahana Ray — exploring one coherent palace, discovering personal memories and messages, opening a special invitation, seeing the crown, and leaving with a royal portrait.
