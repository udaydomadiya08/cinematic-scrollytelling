# Style Synthesis (invent the right style for each project)

The styles in `style-library.md` and the examples in `taste-examples/` are **vocabulary and
calibration, not a menu and not targets.** For every project, design a bespoke style from the subject.
A result that is just "S05 with new text" or "that portfolio with new colors" has failed this step.

## Contents
1. Three ways to arrive at a style
2. The Style Genome (axes with option banks)
3. Procedure (8 steps)
4. Scroll/interaction mechanic catalog
5. Metaphor mining
6. Worked illustrations (not templates)
7. Novelty and fit checks
8. Output: the Style Brief

## 1. Three ways to arrive at a style
- **Seed and mutate:** start from a library style whose signature suits the topic, then change at least three genome
  axes (mechanic, world, type voice, composition, motion temperament) so it becomes its own thing.
- **Hybrid:** combine mechanics and worlds from two or three styles around one signature idea.
- **From scratch:** derive from the subject's own metaphor and physical reality (default when the topic is distinctive).
Prefer from-scratch or hybrid; use a plain library style only when it truly is the best fit, and say why.

## 2. The Style Genome (choose one value per axis; invent new values freely)
| Axis | Option bank (illustrative; extend it) |
|---|---|
| **Subject metaphor** | descent, assembly, orbit, journey, cross-section, growth, erosion, tide, circuit, weave, brewing, signal, archive, map, ladder of scale, machine, organism, performance, ritual |
| **Space / camera** | flat poster, layered depth, single continuous camera, orbit, fly-through, split-screen, pinned stage, tunnel, top-down map, isometric, first-person, macro/micro |
| **Scroll mechanic** | see section 4 (choose the one that *enacts* the metaphor) |
| **Media type** | cinematic film, still photography, 3D real-time, 3D rendered sequence, illustration, SVG line art, typography only, data graphics, procedural/generative, collage |
| **Color world** | derived from subject materials and light: ink + signal, dawn warm neutrals, oxidized metal, deep ocean teal, acid on black, paper + vermilion, glacier white, sodium-lamp amber, monochrome + one hue... |
| **Type voice** | monumental condensed, high-contrast serif, geometric grotesk, humanist text, technical mono, rounded friendly, stencil/industrial, hand-cut, variable-weight kinetic |
| **Material / texture** | glass, paper, film grain, brushed metal, concrete, fabric, liquid, halftone, pixel, none (flat) |
| **Composition** | asymmetric editorial, centered monument, strict grid, broken grid, full-bleed, framed windows, overlapping layers, vertical rails, radial |
| **Motion temperament** | slow/cinematic, snappy/editorial, elastic/playful, mechanical/precise, fluid/organic, glitchy/raw, hushed/luxury |
| **Interaction signature** | pointer tilt, magnetic hover, drag, lens/spotlight, scrubber, click-to-travel, hold-to-reveal, compare slider, parameter sliders |
| **Chrome / navigation** | minimal pill, chapter rail, index list, HUD, none, floating dock, scale bar, timeline |
| **Sound** | silent (default), optional ambient with mute, interaction ticks |
Rule of thumb: at most **one** loud axis per page (the signature); the others support it.

## 3. Procedure
1. **Read the brief**: topic, audience, goal, mood words, User Taste Profile (`intake-questions.md`), assets provided.
2. **Mine metaphors** (section 5): write 5, pick the one with the strongest *visible verb*.
3. **Pick the mechanic** that makes the verb happen on scroll or interaction (section 4).
4. **Pick the world**: color, type voice, material, media type from the subject's real materials, places, and light.
   Run the asset reality check (`asset-pipeline.md`): can the best media for this world be sourced/generated?
   If not, adjust the media type, not the quality bar.
5. **Compose**: decide grid/composition language and at least one inversion or tonal shift for pacing; one still moment.
6. **Set motion temperament** and the small motion language (easing, durations, stagger) - see `motion-and-scroll.md`.
7. **Name the style** (a bespoke name like "Cold Brew Descent" or "Signal Weave") and write one signature sentence.
8. **Check** (section 7); iterate until it passes; write the Style Brief (section 8).

## 4. Scroll / interaction mechanic catalog (pick or combine; invent more)
Scrubbed film; frame-sequence scrub; sticky pinned stage with state changes; chapter snapping; click-to-travel portal /
window expansion; zoom-through / infinite scale; camera fly-through on a path; orbit around an object; exploded/assembly
timeline; parallax depth layers; horizontal film strip; stacking/sliding cards; clip-path / mask reveal; type-as-window;
text fill by scroll; split-screen sync scroll; path-following marker; morphing chart; map pan/zoom; time-scrubber;
parameter sliders controlling a model; cursor-lit reveal; drag-to-explore canvas; compare slider; velocity-reactive
type; number counters tied to progress; scroll-to-type terminal; scroll-driven color/state changes of the whole page;
tilt-to-3D with pointer; hold/press interactions; sound-reactive visuals.

## 5. Metaphor mining
Ask: *What does this subject do, physically? What is it like? What does its audience feel?* List verbs and objects.
- Dig into **materials, tools, places, processes, scales, weather, time** of the subject.
- Look for a **transformation** (raw -> refined, small -> large, hidden -> visible, many -> one, noise -> signal).
- Prefer concrete, filmable metaphors over abstractions ("a bean's journey from cherry to crema" > "premium coffee").
- Reject metaphors that produce the same hero as every other site in the category.

## 6. Worked illustrations (show reasoning, not templates)
- **Black holes explainer** - metaphor: falling inward; mechanic: continuous camera + zoom-through with a
  time-dilation scrubber; world: near-black + lensing amber, mono HUD, thin serif; media: procedural WebGL lensing +
  NASA stills; signature: a clock that slows as you scroll closer.
- **Specialty coffee roaster** - metaphor: roast curve; mechanic: pinned stage where beans change color and a
  temperature curve draws as you scroll; world: kraft paper + roast browns + one tomato-red, hand-cut serif +
  mono; media: macro footage/photography; signature: the roast-curve line is the page's progress bar.
- **Municipal water utility annual report** - metaphor: water's path; mechanic: SVG path-following droplet across a
  map-to-tap journey with data callouts; world: clean blues/white, humanist sans; media: SVG + real stats;
  signature: a single drop that carries you from reservoir to kitchen tap.
- **Chess openings course** - metaphor: a game tree; mechanic: scroll-advanced board with branching lines you can
  hover; world: ink and ivory, tournament-poster type; signature: moves play as you scroll, variations fork.
- **Electric motorbike** - metaphor: current becoming motion; mechanic: frame-sequence teardown with a rider-view
  camera swap; world: matte black + one electric hue; signature: a glowing current path traces the frame.
These illustrate the *method*; for a new request, derive a new idea from that subject.

## 7. Novelty and fit checks
- **Fit:** Does the signature mean something for this subject? Would the audience understand it without help?
- **Distinct:** Remove logo and copy - could it be mistaken for another category's site? For any reference or library entry?
  If yes, change the signature, composition, and type voice (not just color).
- **Not-a-reference:** If a reader could name which `taste-examples/` file or library style it came from, mutate further.
- **Feasible:** Assets and performance support it (`asset-pipeline.md`, `tech-and-performance.md`).
- **One-signature rule:** one loud idea; supporting axes stay quiet.
- **Variety:** differs from other sites built in this conversation on at least three genome axes.
- **Accessible:** reduced-motion state, readable at every progress value, keyboard-usable.

## 8. Output: the Style Brief (<= 12 lines; show to user before building)
```
Style brief - "<bespoke name>"
- Read: <subject> for <audience>, goal <goal>; taste notes: <from user or inferred>
- Metaphor / signature: <one sentence>
- Mechanic: <scroll/interaction>   Space/camera: <...>
- World: palette <roles+hex>, type <display + text (+mono)>, material <...>, composition <...>
- Motion temperament: <...>   Interaction: <...>   Chrome: <...>
- Seeds used (optional): S## / none   Mutations: <3+ axes changed>
- Assets: <real | stock | generated | procedural> with fallbacks
- Assumptions made: <list>   Alternates: <2 other directions in one line each>
```
