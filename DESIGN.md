# DESIGN.md --- The Royal Invitation Experience

> **Purpose:** This document is the implementation-ready design and
> experience specification for the personalised royal invitation
> website. It is written for Claude Code and the development team.
>
> **Primary visual reference:** The screenshots supplied in the
> conversation. Treat those screenshots as the source of truth for the
> visual direction, scene order, composition, and atmosphere.
>
> **Non-negotiable design intent:** Build a stylised, low-poly 3D
> royal-palace journey that feels like an elegant interactive
> adventure/game. Do **not** reinterpret it as a hyper-realistic palace,
> a hotel website, a generic wedding template, or a conventional
> scrolling landing page.

------------------------------------------------------------------------

## 1. Project vision

Create an immersive, personalised digital invitation for **Her Royal
Highness Princess Gahana Ray**. The visitor is invited into a fictional
royal world and progresses through a sequence of palace environments.
The experience should feel thoughtful, cinematic, intimate, playful in
its interaction, and premium in its presentation.

The visitor should feel as though they are entering a small royal
kingdom made especially for one person. The palace is the setting; the
invitation and personal reveal are the emotional purpose.

### Core experience

1.  The visitor arrives outside the palace at sunset.
2.  They choose **APPROACH THE PALACE** to begin.
3.  They enter the grand entrance hall and encounter the staircase.
4.  They move through the Royal Gallery, where personal photographs are
    displayed.
5.  They enter the Grand Ballroom and see a personalised message.
6.  They reach the Rose Garden.
7.  In the garden, they approach and open a special envelope.
8.  The envelope leads into the crown reveal.
9.  The experience ends with an optional live selfie/photo moment using
    a crown overlay.

The screenshots label the five principal chapters as `01 / 05` through
`05 / 05`. Keep those five chapters in the top-level navigation/progress
system. The envelope, crown, and camera are **sequential reveal states
within the final chapter**, not extra top-level chapters unless the
supplied source project already requires otherwise.

### Emotional objectives

-   Create anticipation as the visitor moves from one environment to the
    next.
-   Make the experience feel made specifically for Gahana, not like a
    reusable generic template.
-   Give personal photographs and the final message genuine prominence.
-   Make the envelope and crown reveals feel like rewards at the end of
    the journey.
-   Keep the experience elegant and warm rather than overly ornate or
    visually noisy.

------------------------------------------------------------------------

## 2. Source-of-truth and design guardrails

When making implementation decisions, use this priority order:

1.  The supplied reference screenshots.
2.  This `DESIGN.md`.
3.  Existing project code, assets, and content supplied by the user.
4.  Developer judgement only where the references and this document are
    silent.

### Do not change the aim

Do not: - Replace the interactive palace journey with a normal webpage
or a vertical list of sections. - Change the princess-invitation
concept. - Change the five-chapter structure. - Remove the personal
gallery, ballroom message, Rose Garden, envelope, crown, or camera
finale. - Replace the low-poly/stylised 3D look with photorealism. - Add
unrelated rooms, fantasy creatures, extra storylines, unrelated luxury
motifs, or new narrative chapters. - Make the visual language resemble a
hotel booking site, luxury property listing, generic wedding invitation,
or corporate presentation. - invent event dates, venue details, RSVP
details, dress code, or other invitation facts. Use clearly named
editable placeholders until the owner supplies the final information. -
use the Instagram watermark or the phone's video-editing interface seen
around some screenshots. Those are part of the captured reference media,
not part of the intended product.

### Interpret the reference accurately

The reference is a stylised 3D environment with simplified geometry,
clean silhouettes, warm lighting, and cinematic camera framing. It is
not intended to be a physically exact architectural simulation. The
slight game-like quality is part of its charm and must be preserved.

------------------------------------------------------------------------

## 3. Visual direction

### 3.1 Overall style

**Style keywords:** stylised low-poly 3D, elegant royal adventure,
European palace-inspired architecture, warm sunset, soft golden
interiors, intimate, cinematic, symmetrical, restrained luxury.

The environments should look like carefully art-directed 3D scenes: -
Simplified architectural forms with clean edges and readable
silhouettes. - Deliberate symmetry and strong central perspective. -
Materials that read clearly without excessive texture detail. - Soft,
warm illumination and controlled shadows. - A limited palette of cream,
beige, muted gold, burgundy, deep green, and rose pink/red. - Enough
detail to feel designed, but not so much detail that the scenes become
photorealistic or visually busy.

### 3.2 What "low-poly" means here

Use simplified meshes and forms, but do not make the world crude,
childish, or intentionally jagged. Aim for polished stylisation: -
Walls, columns, windows, balustrades, hedges, and furniture should have
simple, clear geometry. - Trees and shrubs can use rounded or faceted
silhouettes. - Flowers can be stylised meshes or carefully arranged
simple forms. - Chandeliers and the tiara can receive more detail than
the surrounding architecture because they are focal objects. - Use
subtle material variation rather than realistic surface imperfections.

### 3.3 Palette

Use the following as the starting palette. Adjust shades to match the
screenshots and maintain contrast; do not introduce unrelated bright
colours.

  Role                  Colour direction                    Suggested token
  --------------------- ----------------------------------- -----------------------
  Main architecture     Warm ivory / cream                  `#E8D8C5`
  Lit architecture      Pale champagne                      `#F3E5D3`
  Shadow architecture   Warm taupe                          `#A88D78`
  Burgundy              Deep wine / oxblood                 `#4A1720`
  Carpet                Dark burgundy                       `#4B1722`
  Gold details          Muted antique gold                  `#B89A62`
  Garden hedges         Deep muted green                    `#27351F`
  Lawn                  Olive green                         `#45451F`
  Roses                 Deep red and dusty pink             `#9B2637` / `#C9797B`
  Sunset                Peach, rose, apricot, muted mauve   gradient
  UI text               Warm white                          `#F6EEE5`
  UI hairlines          Muted gold                          `#B89A62`

These are design tokens, not a requirement to force every object to one
exact hex value. Keep the overall image warm and cohesive.

### 3.4 Lighting and atmosphere

-   Exterior scenes: sunset or golden-hour lighting with a peach-to-rose
    sky. The first scene can be duskier and more mauve; the final garden
    can be brighter and more golden.
-   Interior scenes: warm amber/champagne illumination, with chandeliers
    as visible practical light sources.
-   Use soft ambient fill so architectural details remain readable.
-   Shadows should be present but not harsh or black.
-   Avoid cold blue lighting, neon, dramatic horror contrast, or
    high-gloss reflective surfaces.
-   Keep bloom subtle or omit it if it reduces text and object clarity.

### 3.5 Camera language

The experience is presented from a first-person visitor perspective, not
as a detached architectural fly-through.

-   Use a deliberate central axis in the symmetrical scenes.
-   Prefer slow forward movement and gentle camera easing.
-   Use restrained rotations to reveal objects; do not spin, whip-pan,
    or shake the camera.
-   Keep the visitor's point of view at a plausible standing height.
-   Ensure the key object remains in the centre or clearly readable
    region of the frame.
-   The camera should never clip through walls, stairs, frames,
    pedestals, hedges, or other geometry.
-   Camera motion must be interruptible or skippable where practical,
    and must not prevent access to the invitation content.

------------------------------------------------------------------------

## 4. Experience structure and scene specifications

## Chapter 01 --- THE ARRIVAL (`01 / 05`)

### Purpose

Establish the royal world and invite the visitor to enter.

### Environment

-   A symmetrical European palace façade, viewed from the centre of the
    front garden.
-   The palace should be wide, stately, and composed around a central
    entrance and slightly raised central roof section.
-   Repeated windows and wings on both sides create symmetry.
-   A central pathway leads from the foreground directly to the palace
    entrance.
-   Formal garden beds and clipped hedges frame the pathway.
-   Small topiary/conical trees and restrained garden details can be
    used.
-   The sky is a warm dusk gradient: muted mauve/rose above,
    transitioning to peach/apricot near the horizon.
-   The building is lit warmly from within; windows glow softly.

### Composition

-   Vertical 9:16 composition.
-   Palace centred on the horizontal axis.
-   Pathway begins in the foreground and guides the eye to the central
    entrance.
-   Keep the centre area readable for the invitation typography.
-   Do not let garden objects obstruct the title or primary CTA.

### On-screen content

-   Chapter label: `THE ARRIVAL · 01 / 05`
-   Eyebrow: `AN INVITATION`
-   Honorific: `Her Royal Highness`
-   Main name: `Princess Gahana Ray`
-   Supporting line: `A special evening awaits.`
-   Primary CTA: `APPROACH THE PALACE`
-   Secondary action: `SKIP INTRO`

All text must be editable from a central content/configuration file.
Preserve the line breaks and hierarchy shown in the reference. Use an
elegant high-contrast serif for the princess's name and a restrained
sans-serif for labels and supporting UI.

### Interaction

-   `APPROACH THE PALACE` starts the journey and triggers the transition
    into Chapter 02.
-   `SKIP INTRO` skips the opening camera/intro animation and moves to
    the next usable state. It must not skip or hide the actual
    invitation content.
-   The sound icon toggles audio on/off.
-   The chapter indicator and decorative progress motif remain
    consistent with the other scenes.

### Motion

-   Begin with a stable establishing view.
-   A subtle slow camera push towards the palace is acceptable.
-   On CTA activation, move smoothly towards/into the entrance and
    transition to Chapter 02.
-   Do not make the opening camera movement so slow that the visitor
    feels stuck.

------------------------------------------------------------------------

## Chapter 02 --- THE GRAND ENTRANCE (`02 / 05`)

### Purpose

Make the visitor feel they have entered the palace.

### Environment

Recreate the grand entrance shown in the reference: - Large, symmetrical
interior hall. - Broad central staircase rising towards a tall, dark
burgundy arched doorway. - A burgundy carpet runs up the central
staircase and continues through the foreground. - Cream/beige stone or
plaster walls. - Tall, narrow arched windows on either side, softly
lit. - Balustrades and stair rails on both sides. - A large chandelier
hanging from the centre of the ceiling. - A circular ceiling
detail/medallion above the chandelier. - Checkered cream-and-dark-brown
marble floor in the foreground. - Decorative spherical finials at the
staircase/landing edges.

### Composition

-   Camera faces the staircase directly, centred on the carpet.
-   The staircase and dark arched doorway are the main focal point.
-   Keep the chandelier visible overhead.
-   The checkered floor anchors the foreground and helps establish
    scale.
-   Preserve strong left-right symmetry.

### Interaction and transition

-   The visitor progresses forward towards the staircase/landing.
-   Use a short, smooth transition from Chapter 01 into this hall.
-   Provide a clear next/continue interaction if the experience is not
    fully auto-progressing.
-   Do not require precision mouse movement to advance.

### Motion

-   Slow forward dolly towards the staircase.
-   If the staircase is traversed, camera movement should follow the
    centre of the stairs without clipping.
-   The next transition leads into the Royal Gallery.

------------------------------------------------------------------------

## Chapter 03 --- THE ROYAL GALLERY (`03 / 05`)

### Purpose

Make the experience personal by displaying photographs of Gahana and the
people/memories selected by the owner.

### Environment

Recreate the long corridor in the reference: - Long, symmetrical gallery
corridor. - Repeated curved/arched ceiling bays receding into the
distance. - A series of chandeliers down the centre line. - Burgundy
wall panels and deep burgundy end wall. - Cream/beige architectural trim
and columns. - Tall arched windows alternating with framed
photographs/artworks. - Framed photographs placed at a consistent
viewing height. - Small pedestal/bust-like decorative objects may sit
below or near selected frames. - Warm parquet or patterned wood
flooring. - A burgundy runner carpet down the centre. - A pair of doors
or a clear endpoint at the far end.

### Composition

-   Strong one-point perspective down the centre of the corridor.
-   The central runner leads the eye towards the far doors.
-   Frames are visible on both walls.
-   Keep the frames large enough to recognise the photographs on a phone
    screen.
-   The corridor should feel long and elegant, but not endless.

### Personal photographs

-   Use owner-provided photographs only.
-   Do not invent or generate substitute people for the personal
    gallery.
-   Create a data-driven gallery so the owner can replace images without
    editing scene logic.
-   Preserve aspect ratios; use a tasteful crop/fit mode per image.
-   Use a consistent frame treatment (warm wood/antique gold) and
    restrained lighting.
-   If a photograph is missing, show a neutral placeholder frame that
    does not look like a broken image.
-   Do not hard-code image paths into scene components; load them from
    the content configuration.

### Interaction

-   The visitor can approach or select a frame to view the photograph
    more clearly.
-   If a photo opens in an enlarged view, provide an obvious close/back
    action.
-   Selecting a frame must not accidentally advance to another chapter.
-   Use subtle highlight/lighting or a gentle scale change to indicate
    an interactive frame.
-   The experience must remain usable on touchscreens; do not rely only
    on hover.

### Motion

-   Smooth camera travel down the corridor.
-   Optionally pause briefly at selected photographs if this is part of
    the existing source experience.
-   Avoid automatically lingering so long that the visitor loses
    control.
-   Transition through the far end of the gallery into the Grand
    Ballroom.

------------------------------------------------------------------------

## Chapter 04 --- THE GRAND BALLROOM (`04 / 05`)

### Purpose

Create a quiet ceremonial pause and present the central personalised
message.

### Environment

Recreate the ballroom in the reference: - Large open rectangular room. -
Cream/champagne walls with restrained rectangular moulding/panel
details. - Warm wooden parquet floor with a geometric block pattern. -
Large central chandelier. - A symmetrical focal arrangement at the far
end. - A central burgundy/dark plaque or freestanding sign on a stand. -
Two matching flower arrangements on either side of the sign. - A
circular or oval floor inlay/ring can frame the central display, as in
the reference.

### Central message plaque

The reference shows the message:

`A little kingdom, made for one very special girl`

Treat this as the default reference copy. It must remain editable. Any
smaller secondary text that is not legible in the supplied screenshot
must not be invented; leave it configurable/blank until supplied.

### Composition

-   Centre the plaque on the room's main axis.
-   Keep the chandelier above the plaque in the visual hierarchy.
-   Flowers should balance the plaque, not compete with it.
-   Ensure the message can be read at mobile size.
-   Do not cover the plaque with chapter UI or decorative symbols.

### Interaction

-   The visitor approaches the plaque.
-   The plaque may reveal its message with a gentle fade/lighting
    emphasis.
-   Continue action moves the visitor towards the Rose Garden.

### Motion

-   Gentle forward camera push.
-   Subtle pause when the message is fully in view.
-   No rapid zoom or dramatic camera shake.

------------------------------------------------------------------------

## Chapter 05 --- THE ROSE GARDEN (`05 / 05`)

### Purpose

Deliver the most beautiful outdoor environment and host the final
invitation reveals.

### Environment

Recreate the garden in the reference: - Formal, symmetrical royal
garden. - Central pale stone pathway leading towards a circular fountain
and a white domed gazebo/pavilion. - Palace façade visible in the
background. - Tall clipped hedges and rounded topiary on both sides. -
Long flower beds with red and pink roses. - Repeated small trees/topiary
in planters along the path. - Pale stone edging and formal garden
geometry. - Warm peach/pink/golden sunset sky. - The garden should feel
open, romantic, and calm.

### Composition

-   Strong central perspective.
-   Central path, fountain/gazebo, and palace aligned.
-   Roses and hedges frame the path without obscuring the central
    structure.
-   The garden should be the most open and visually uplifting scene.
-   Maintain the low-poly stylised geometry used throughout.

### Garden copy

The reference includes:

`Every rose here is yours.`

Use this as the default garden line. Keep it editable. Display it in a
graceful serif style, with enough contrast against the background.

### Interaction

-   The visitor can move/advance along the path.
-   The camera approaches the central gazebo/fountain.
-   The envelope reveal is triggered at the designated pedestal.
-   The garden remains the environment behind the envelope and crown
    states unless the supplied source project specifies a different
    transition.

------------------------------------------------------------------------

## 5. Final reveal states within Chapter 05

These are essential parts of the experience and must not be omitted.

### 5.1 Envelope reveal

#### Visual

-   A pale circular or softly rounded marble pedestal/table.
-   The envelope sits centrally on the pedestal.
-   Two small candle-like decorative objects sit to one side.
-   A small flower arrangement sits to the other side.
-   The object is illuminated by a soft pool of warm light.
-   The background remains consistent with the Rose Garden/palace
    environment.
-   A clear `OPEN THE ENVELOPE` CTA appears near the lower part of the
    screen, matching the elegant UI style.

#### Interaction

-   The visitor approaches the pedestal.
-   The envelope is the primary interactive object.
-   Activating `OPEN THE ENVELOPE` opens/reveals the invitation content.
-   Use a deliberate envelope-opening animation if feasible: slight
    lift, flap movement, and/or a letter emerging. Keep it smooth and
    understated.
-   Do not make the envelope animation block access to the message for
    an excessive duration.
-   The invitation content must be actual readable text, not only an
    image of text.
-   All event-specific details must come from editable content fields.
    Do not fabricate missing details.

#### Content fields to support

Use optional fields, only displaying those supplied: - Event
title/name - Date - Time - Venue - Address/location - Dress code - RSVP
contact/instructions - Additional personal message

If a field is not supplied, omit it cleanly. Do not show `TBD`, fake
dates, or dummy contact details in the final production experience.

### 5.2 Crown reveal

#### Visual

-   A silver/diamond tiara placed on a rich burgundy velvet cushion.
-   Cushion rests on a clean pale marble pedestal.
-   The tiara is delicate, feminine, and recognisably royal.
-   It should have a clear silhouette and visible sparkle/highlights
    without looking oversized or cartoonish.
-   The scene is slightly darker/more intimate than the open garden, as
    shown in the reference.
-   The crown is the hero object: do not surround it with unnecessary
    jewellery or props.

#### Interaction and motion

-   After the envelope/invitation reveal, transition to the crown.
-   Slowly push the camera towards the tiara.
-   A subtle glint or restrained sparkle may be used.
-   Do not use flashing effects or excessive particles.
-   Preserve the crown as a separate visual reveal, not merely a static
    icon.

### 5.3 Live selfie / camera finale

#### Visual

-   Request access to the visitor's front-facing camera only when they
    choose to enter this feature.
-   Display a live camera preview in a clean, intentional frame.
-   Add a silver diamond tiara overlay aligned above the visitor's
    forehead.
-   The crown should follow the head position/rotation using face
    tracking where supported.
-   The crown overlay must be visually consistent with the crown
    revealed in the previous scene.
-   Provide clear capture and close/exit controls.

#### Functionality

-   Camera permission must be requested at the moment the visitor
    chooses the camera feature, not immediately on page load.
-   If permission is denied or the device has no camera, show a polite
    fallback state and allow the visitor to continue without a photo.
-   Do not upload, save, or transmit camera images unless the owner
    explicitly implements and discloses that functionality.
-   Prefer local/on-device processing for face tracking.
-   Provide a capture action and a way to save/download the captured
    image if technically supported.
-   Provide a retake action.
-   Provide a clear way to exit the camera experience.
-   Do not make the camera feature mandatory to finish the invitation.
-   On devices/browsers without face-tracking support, use a reasonable
    centred crown overlay or offer a static photo frame rather than
    failing.

------------------------------------------------------------------------

## 6. Persistent user interface

### 6.1 Chapter header

The top of each scene should preserve the reference's understated
header: - Chapter name in uppercase. - Chapter number, formatted as
`01 / 05`, `02 / 05`, etc. - Small, thin progress marks/lines beneath or
near the chapter label. - Back arrow where appropriate. - Sound toggle
at the top-right.

Examples: - `THE ARRIVAL · 01 / 05` - `THE GRAND ENTRANCE · 02 / 05` -
`THE ROYAL GALLERY · 03 / 05` - `THE GRAND BALLROOM · 04 / 05` -
`THE ROSE GARDEN · 05 / 05`

### 6.2 Blue eye-shaped motif

The screenshots show a horizontal row of nine blue evil-eye symbols near
the top of the scene.

-   Preserve this motif as a recognisable decorative signature of the
    reference.
-   Use nine evenly spaced symbols, matching the reference count.
-   Keep their scale, spacing, and horizontal alignment consistent
    across chapters.
-   They are decorative unless the existing implementation explicitly
    uses them as controls.
-   Do not reinterpret them as a loading spinner or replace them with
    generic dots.
-   They should not overpower the chapter label or block the main scene.
-   On narrow screens, scale them down or reduce spacing while retaining
    all nine symbols if possible.

### 6.3 Typography

Use two complementary families: 1. **Display serif:** elegant,
high-contrast serif for the princess's name, invitation lines, and
emotional messages. 2. **UI sans-serif:** clean, restrained sans-serif
for chapter labels, controls, and secondary information.

Typography behaviour: - Main name is the largest text on the opening
screen. - Chapter labels use uppercase, letter spacing, and small
sizing. - Buttons use uppercase lettering and generous tracking. - Avoid
too many font styles or weights. - Do not use novelty, handwritten, or
cartoon fonts. - Ensure all text remains legible on a phone.

Use licensed/web-safe fonts or locally bundled fonts with a suitable
fallback stack. Do not depend on a remote font being available for the
experience to render.

### 6.4 Buttons and controls

-   Rectangular or subtly rounded outlined CTA style, as in the
    reference.
-   Thin muted-gold border.
-   Transparent or lightly tinted background.
-   Warm-white text.
-   Clear hover, focus, pressed, and disabled states.
-   Large enough touch target for mobile use.
-   No oversized pill buttons unless already present in the supplied
    project.
-   Do not use generic dashboard-style controls.

### 6.5 UI placement and safe areas

-   Respect mobile safe areas, including notches and home indicators.
-   Keep top controls away from the device status/notch region.
-   Keep bottom CTAs above the home indicator.
-   Keep important text away from the extreme left/right edges.
-   Do not let the UI overlap the key 3D object.
-   Maintain the reference's vertical composition at 9:16 while adapting
    carefully to other aspect ratios.

------------------------------------------------------------------------

## 7. Navigation, state, and interaction model

### Top-level chapter state

Use five principal chapter states:

``` text
ARRIVAL
  -> GRAND_ENTRANCE
  -> ROYAL_GALLERY
  -> GRAND_BALLROOM
  -> ROSE_GARDEN
```

### Final chapter sub-states

``` text
ROSE_GARDEN
  -> ENVELOPE_APPROACH
  -> ENVELOPE_OPEN
  -> CROWN_REVEAL
  -> CAMERA_EXPERIENCE (optional)
  -> COMPLETION
```

The camera experience is optional. The visitor must still be able to
finish after viewing the crown.

### Navigation requirements

-   Provide a clear forward path through the experience.
-   Back navigation should return to the previous meaningful state
    without unexpectedly resetting the entire journey.
-   The visitor should be able to skip non-essential camera animations.
-   Do not allow a double-click or repeated tap to trigger duplicate
    transitions.
-   Disable or guard scene-changing actions while a transition is
    already in progress.
-   Preserve the current chapter and reveal state on resize/orientation
    change.
-   If a page refresh resets the experience, restart cleanly at the
    arrival scene unless persistence is intentionally implemented.
-   Avoid trapping the visitor in a scene or modal.

### Input support

Support: - Touch/tap on phones and tablets. - Mouse click on desktop. -
Keyboard activation for buttons and interactive objects where
practical. - Visible focus states for keyboard navigation.

Do not require hover to discover an essential action.

------------------------------------------------------------------------

## 8. Motion and transitions

### General motion principles

-   Smooth, slow, elegant, cinematic.
-   Use easing rather than linear movement for camera transitions.
-   Keep animations purposeful and relatively short.
-   Avoid bounce, elastic easing, exaggerated parallax, fast spins, and
    excessive particle effects.
-   Respect the user's reduced-motion preference.

### Suggested transition language

-   Chapter-to-chapter: gentle fade combined with a camera move or a
    controlled crossfade.
-   Arrival-to-entrance: forward approach through the palace entrance.
-   Entrance-to-gallery: move through the central doorway.
-   Gallery-to-ballroom: move towards the far doors and transition.
-   Ballroom-to-garden: warm fade/doorway transition into the garden.
-   Garden-to-envelope: controlled approach to the pedestal.
-   Envelope-to-crown: intimate, soft fade or object-led reveal.
-   Crown-to-camera: transition into a clean camera frame.

Do not use abrupt hard cuts unless required by performance or browser
constraints.

### Timing guidance

Treat timings as starting points, not rigid requirements: - Small UI
fades: approximately 200--400 ms. - Scene transitions: approximately
700--1,400 ms. - Camera approach: approximately 1,500--3,000 ms
depending on distance. - Object reveal: approximately 500--1,200 ms.

Allow the user to proceed without waiting for a long cinematic
animation.

------------------------------------------------------------------------

## 9. Audio

-   The reference includes a sound toggle.
-   Provide a persistent sound on/off control.
-   Audio must not autoplay with sound before the visitor interacts with
    the page; follow browser autoplay restrictions.
-   If background music is supplied, use it at a restrained volume.
-   If sound effects are supplied, use them sparingly for transitions,
    envelope opening, or the crown reveal.
-   Do not invent a recognisable copyrighted song or imitate a specific
    commercial soundtrack.
-   If no audio assets are supplied, the experience must still feel
    complete and must not show a broken audio control.
-   Remember the user's sound preference during the current session
    where practical.

------------------------------------------------------------------------

## 10. Responsive behaviour

### Primary target

Mobile portrait, 9:16. The screenshots are vertical mobile references,
so this is the primary design target.

### Secondary targets

-   Desktop browser.
-   Tablet portrait and landscape.
-   Mobile landscape where practical.

### Responsive rules

-   Preserve the central axis and key composition.
-   Keep the palace, staircase, corridor, plaque, envelope, and crown
    visible.
-   Scale typography and controls without changing the hierarchy.
-   Reposition UI only when needed to avoid covering the scene's focal
    point.
-   Do not simply crop the top and bottom of the 3D scene on desktop.
-   Use an adaptive camera field of view or framing so the scene remains
    composed.
-   Keep buttons and touch targets comfortably tappable.
-   Ensure the gallery photographs remain visible and selectable.
-   On lower-powered mobile devices, reduce shadow resolution,
    post-processing, and decorative detail before reducing essential
    content.

------------------------------------------------------------------------

## 11. Technical implementation direction

### Preferred stack

Use the existing project stack if it is already established. If starting
from a new project, the intended direction is:

-   React for UI and application state.
-   Three.js for 3D rendering.
-   React Three Fiber for declarative Three.js scene composition.
-   Drei for common scene helpers where useful.
-   CSS for the interface overlay and responsive typography.
-   A suitable lightweight animation solution (for example, React Spring
    or GSAP) for camera and UI transitions, without introducing
    unnecessary competing animation systems.

Do not migrate or replace an existing working stack without a clear
technical reason.

### Architecture principles

Keep the implementation modular. Separate: - Application shell and
routing/state. - 3D canvas and scene composition. - Individual chapter
environments. - Camera choreography. - UI overlay and controls. -
Personal photographs and content. - Audio handling. - Camera permission
and face-tracking functionality.

Suggested conceptual structure (adapt to the repository rather than
forcing exact filenames):

``` text
src/
  app/
    App
    experienceState
    content
  components/
    ChapterHeader
    EyeMotif
    SceneTransition
    PrimaryButton
    SoundToggle
  scenes/
    ArrivalScene
    GrandEntranceScene
    RoyalGalleryScene
    GrandBallroomScene
    RoseGardenScene
  reveals/
    EnvelopeReveal
    CrownReveal
    CameraExperience
  camera/
    CameraRig
    cameraPaths
  assets/
    models/
    textures/
    photographs/
    audio/
  styles/
    tokens
    global
```

### Scene construction

-   Each scene should be an independently maintainable component or
    module.
-   Reuse shared materials and repeated geometry where possible.
-   Reuse a consistent lighting setup where it makes sense, but allow
    the exterior and interior scenes to have their own lighting
    settings.
-   Keep the camera rig separate from individual scene geometry.
-   Avoid putting all scene logic into one giant component.
-   Keep content and assets configurable.
-   Do not create a large number of expensive real-time lights if baked
    lighting or simpler lighting can achieve the reference look.

### 3D assets

-   Prefer optimised GLB/GLTF models for complex hero assets where
    appropriate.
-   Use procedural geometry for repeated/simple architecture when that
    is more efficient.
-   Reuse geometry and materials for repeated windows, columns, hedges,
    flowers, and frames.
-   Keep polygon counts appropriate for mobile.
-   Compress models and textures where supported.
-   Use texture atlases or shared materials where practical.
-   Ensure model origins, scales, and pivots are correct for animation.
-   Avoid loading multiple huge versions of the same asset.

### Personal content configuration

Keep personal copy, photographs, and event details in one clearly
documented configuration/data layer. Example shape:

``` js
export const invitationContent = {
  honoree: {
    honorific: "Her Royal Highness",
    displayName: "Princess Gahana Ray",
  },
  opening: {
    eyebrow: "AN INVITATION",
    supportingLine: "A special evening awaits.",
    primaryAction: "APPROACH THE PALACE",
    secondaryAction: "SKIP INTRO",
  },
  ballroom: {
    message: "A little kingdom, made for one very special girl",
  },
  garden: {
    message: "Every rose here is yours.",
  },
  event: {
    title: "",
    date: "",
    time: "",
    venue: "",
    address: "",
    dressCode: "",
    rsvp: "",
    additionalMessage: "",
  },
  gallery: [
    // { id: "photo-01", src: "/assets/photographs/photo-01.jpg", alt: "..." }
  ],
};
```

This is a conceptual schema. Adapt to the codebase's conventions. Do not
place empty event fields visibly in the production UI.

### Camera and face tracking

-   Keep the camera experience isolated from the 3D chapter renderer
    where possible.
-   Request camera permission only after the visitor chooses the selfie
    feature.
-   Use a maintained face-landmark/face-tracking library compatible with
    the chosen stack and browser support.
-   Track face position and head rotation, then position/rotate/scale
    the tiara overlay accordingly.
-   Smooth tracking data to reduce jitter.
-   Handle no-face, multiple-face, lost-face, and permission-denied
    states gracefully.
-   Stop camera tracks when the camera view is closed or the experience
    is left.
-   Do not store or transmit camera frames by default.

------------------------------------------------------------------------

## 12. Performance and reliability

The experience must be designed for mobile browsers, not only a powerful
desktop.

### Performance requirements

-   Optimise 3D models, textures, lighting, and shadows.
-   Lazy-load later scenes and heavy assets where practical.
-   Preload only what is needed for the opening scene and the next
    transition.
-   Show a restrained loading state if a scene needs time to load.
-   Avoid layout shifts while assets load.
-   Dispose of unused geometries, materials, textures, and render
    targets when scenes are removed.
-   Avoid unnecessary React re-renders in the animation/render loop.
-   Reuse objects and assets across scenes.
-   Prefer efficient instancing for repeated objects such as hedges,
    roses, windows, and balusters.
-   Test on a mid-range mobile device, not only a desktop development
    machine.

### Fallback behaviour

-   If WebGL is unavailable, show a graceful fallback with the
    invitation copy and a clear route to the event details.
-   If a 3D asset fails, use a neutral placeholder or simplified
    procedural replacement rather than a blank scene.
-   If a photograph fails to load, preserve the frame and show a neutral
    fallback.
-   If camera permission is denied, allow the visitor to continue
    without the selfie feature.
-   If audio is unavailable, the experience remains fully usable.

### Error handling

-   No unhandled runtime errors when moving between chapters.
-   No stuck loading state.
-   No duplicate scene transitions.
-   No camera left running after exit.
-   No console errors from missing assets in the final build.

------------------------------------------------------------------------

## 13. Accessibility and usability

-   Use semantic HTML for interface controls.
-   Buttons must be keyboard operable.
-   Provide visible focus states.
-   Ensure readable contrast over the 3D scene; use subtle text shadows
    or local gradients only when necessary.
-   Respect `prefers-reduced-motion`.
-   Provide a way to skip long camera movements.
-   Do not make essential information available only through audio,
    animation, or a photograph.
-   Keep event details as real selectable text.
-   Provide meaningful alt text for personal gallery images where
    appropriate.
-   Camera access must be optional and clearly explained.
-   Provide clear permission-denied and unsupported-device messages.

------------------------------------------------------------------------

## 14. Content and asset checklist

The implementation should support these owner-supplied assets:

### Required or strongly recommended

-   Palace exterior reference/model or scene assets.
-   Grand entrance staircase/hall assets.
-   Royal Gallery corridor assets.
-   Personal gallery photographs.
-   Grand Ballroom assets.
-   Rose Garden assets.
-   Envelope model/texture.
-   Silver diamond tiara model/asset.
-   Optional background music and sound effects.
-   Final event details and invitation copy.
-   Optional logo/monogram if the owner supplies one.

### Asset handling

-   Do not invent personal photographs.
-   Do not invent the event date, venue, address, or RSVP contact.
-   Use clearly named placeholders during development.
-   Keep asset names and content IDs understandable.
-   Use compressed formats appropriate for web delivery.
-   Check every asset on mobile for legibility and correct crop.

### Image framing

-   Gallery images should use consistent frames and a deliberate crop
    strategy.
-   Avoid stretching photographs.
-   Use `object-fit: cover` or an equivalent crop only when it preserves
    the important subject.
-   Allow portrait and landscape images to be handled gracefully.
-   The tiara should retain its silhouette and sparkle at mobile
    resolution.

------------------------------------------------------------------------

## 15. Quality assurance and acceptance criteria

Do not consider the experience complete until all of the following are
checked.

### Visual fidelity

-   [ ] The overall experience reads as stylised low-poly 3D, not
    photorealistic.
-   [ ] The palette matches the warm cream, burgundy, muted gold, deep
    green, and sunset reference.
-   [ ] The opening palace is symmetrical and centred.
-   [ ] The grand entrance includes the staircase, burgundy runner,
    checkered floor, arched doorway, and chandelier.
-   [ ] The Royal Gallery includes the vaulted ceiling, chandeliers,
    burgundy walls, arched windows, central runner, and personal photo
    frames.
-   [ ] The Grand Ballroom includes the chandelier, parquet floor,
    symmetrical wall details, central message plaque, and flower
    arrangements.
-   [ ] The Rose Garden includes the palace backdrop, formal hedges,
    roses, pathway, fountain, and domed gazebo.
-   [ ] The envelope appears on its own pedestal with the supporting
    decorative details.
-   [ ] The crown appears on a burgundy cushion on a pale pedestal.
-   [ ] The camera finale shows the visitor with the tiara overlay when
    permission and tracking are available.
-   [ ] The nine blue eye-shaped symbols and five-chapter progress
    treatment are preserved.

### Functional flow

-   [ ] The visitor can start from the arrival screen.
-   [ ] `APPROACH THE PALACE` advances into the experience.
-   [ ] `SKIP INTRO` skips only the intro movement, not essential
    content.
-   [ ] All five chapters are reachable in the correct order.
-   [ ] Back and continue controls behave predictably.
-   [ ] Gallery photographs can be opened and closed.
-   [ ] Ballroom message is readable.
-   [ ] Garden message is readable.
-   [ ] Envelope can be opened.
-   [ ] Invitation details are real text and are configurable.
-   [ ] Crown reveal is shown after the envelope sequence.
-   [ ] Camera feature is optional.
-   [ ] Camera permission denial does not block completion.
-   [ ] Sound toggle works.
-   [ ] The experience can be completed on touch and mouse devices.

### Technical and responsive

-   [ ] Mobile portrait 9:16 is the primary polished layout.
-   [ ] Desktop and tablet layouts remain composed and readable.
-   [ ] No important UI is hidden by device safe areas.
-   [ ] No scene clips the camera through geometry.
-   [ ] Scene changes do not cause duplicate transitions or crashes.
-   [ ] Heavy assets are optimised/lazy-loaded.
-   [ ] Reduced-motion preference is respected.
-   [ ] WebGL/camera/audio failure states are handled gracefully.
-   [ ] Camera tracks stop when the selfie feature closes.
-   [ ] Final production build has no missing assets or blocking console
    errors.

------------------------------------------------------------------------

## 16. Development workflow for Claude Code

Claude Code should work in this order:

1.  **Inspect the repository first.** Identify the current framework,
    existing routes, components, assets, scripts, and dependencies. Do
    not overwrite or replace a working setup without a reason.
2.  **Map existing work to this specification.** Identify what is
    already implemented and what is missing.
3.  **Create the five-chapter experience state model.** Ensure the
    reveal states are nested within Chapter 05.
4.  **Implement the persistent UI system.** Chapter header, progress,
    nine-eye motif, sound toggle, navigation, and CTA styling.
5.  **Build the environments in order.** Arrival, Grand Entrance, Royal
    Gallery, Grand Ballroom, Rose Garden.
6.  **Add the personal gallery using configurable image data.**
7.  **Implement the ballroom and garden messages.**
8.  **Build the envelope interaction and editable invitation content.**
9.  **Build the crown reveal.**
10. **Implement the optional camera/selfie experience with robust
    permission and fallback handling.**
11. **Add camera choreography, scene transitions, audio, responsive
    behaviour, and reduced-motion support.**
12. **Optimise and test on mobile.**
13. **Run the production build and resolve errors.**
14. **Document how to replace photographs, edit invitation copy, add
    event details, and replace 3D/audio assets.**

### Claude Code working rules

-   Read the existing project before changing files.
-   Preserve the project's current purpose and existing useful work.
-   Do not perform a wholesale redesign.
-   Do not silently remove any scene or interaction in this document.
-   Do not replace actual 3D environments with static background images
    as the final implementation.
-   Temporary mock geometry is acceptable during development, but label
    it as temporary and replace it before completion.
-   Do not fabricate personal content or event facts.
-   If a required asset or event detail is unavailable, implement a
    documented placeholder/configuration slot and continue.
-   Keep components readable and modular.
-   After implementation, report what is complete, what remains, which
    assets/content the owner must provide, and how to run the project.

------------------------------------------------------------------------

## 17. Final creative test

Before calling the work finished, compare the running experience
side-by-side with the supplied screenshots.

Ask:

1.  Does the first screen immediately feel like the same royal
    invitation world?
2.  Does the palace look stylised and game-like rather than
    photorealistic?
3.  Is the central perspective and symmetry preserved?
4.  Do the staircase, gallery, ballroom, and garden match the reference
    compositions?
5.  Are the personal photographs and messages treated as the emotional
    centre of the experience?
6.  Does the visitor feel that they are moving through one connected
    palace, rather than clicking through unrelated web pages?
7.  Does the envelope-to-crown-to-selfie finale feel like a coherent
    reveal?
8.  Is every important action clear on a phone?
9.  Has anything been added that changes the original aim?

If the answer to the final question is yes, remove the unrelated
addition and return to the reference.

**The finished product should feel like stepping into a beautifully
stylised royal invitation made especially for Princess Gahana Ray ---
not browsing a website about a palace.**
