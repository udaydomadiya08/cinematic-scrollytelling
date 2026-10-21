# Art Direction Reference

## Contents
1. Finding the signature idea
2. Archetypes (pick, then bend)
3. Palette
4. Typography
5. Composition and layout
6. Imagery, lighting, materials
7. Hierarchy per scene
8. Subject-specific starting points
9. Anti-template list

## 1. Finding the signature idea
One memorable device the whole experience orbits. Ask: *What is the single image or movement a visitor would describe to a friend?*
Examples of signature ideas (do not reuse verbatim; derive your own):
- A continuous camera descent through layers (atmosphere -> structure -> component -> material).
- A subject that is progressively assembled or dissected as you scroll.
- Type that behaves as architecture: giant letterforms act as windows, masks, or floors.
- A single scrubbed scalar (time, temperature, scale) that re-skins the whole scene.
- A map/terrain that becomes the interface.
- A lens or flashlight that reveals the "real" layer beneath.
Test: remove the logo and copy; is the page still recognizable? If not, push further.

## 2. Archetypes (choose one, then mix deliberately)
- **Editorial / monumental type** - oversized display type, asymmetry, tight crops, hairline rules.
- **Technical / blueprint** - fine grids, callouts, mono annotations, orthographic views.
- **Documentary / photographic** - full-bleed real imagery, grain, restrained UI, captions.
- **Industrial / material** - texture, macro detail, heavy weight type, physical lighting.
- **Scientific / instrument** - data-forward, calm palette, precise labeling, units shown.
- **Playful / kinetic** - saturated color, elastic type, toy-like interaction (only when the brand is).
- **Luxury / quiet** - generous negative space, slow easing, minimal palette, one hero object.
- **Retro-future / archival** - period type, paper/film textures, annotated diagrams.
Dark mode, light mode, or mid-tone is a decision tied to the subject and viewing context, not a default.

## 3. Palette
- 1 dominant ground, 1 ink, 1 accent, 1-2 supporting tones, 1 signal color for states/data.
- Define as CSS custom properties with roles (`--ground`, `--ink`, `--accent`, `--signal`, `--muted`).
- Check contrast: body text >= 4.5:1, large text >= 3:1, UI components >= 3:1.
- Derive the palette from the subject (material, environment, instrument, brand) rather than from a trend.
- Use accent sparingly; scarcity makes it meaningful.

## 4. Typography
- Pair intentionally: a distinctive display face + a highly legible text face (+ mono for data/labels if useful). Two families is usually enough.
- Use a fluid type scale (`clamp()`), tight display leading (0.85-1.05), generous text leading (1.45-1.65), measure 45-75ch.
- Display type can be an image: crop it, mask it, outline it, let it overlap objects with correct z-order.
- Load fonts responsibly: subset, `font-display: swap` (or `optional` for display), preload the one critical file, define metric-matched fallbacks to prevent layout shift.
- Verify licenses for any font used. Prefer open-licensed (e.g. Fontshare, Google Fonts, Open Foundry) when no license is supplied.

## 5. Composition and layout
- Choose a grid (12-col, modular, or deliberately broken) and state the rule you break and why.
- Alternate: full-bleed, asymmetric editorial, split comparison, technical close-up, panoramic, diagram, still moment.
- Use scale contrast (tiny label next to monumental number), overlap, cropping, and edge tension.
- Negative space is a tool: give the focal subject room and let silence pace the story.
- Mobile is a re-composition, not a shrink: reorder, crop differently, change scene lengths, simplify interactions.

## 6. Imagery, lighting, materials
- Keep one lighting logic across all assets (direction, hardness, color temperature).
- Unify disparate sources with a consistent grade (LUT/CSS filter/blend), grain, and aspect rules.
- Prefer real photography/footage or high-quality renders to generic stock. Avoid obviously AI-artifacted imagery; inspect at full size.
- For 3D: believable materials (roughness/metalness), HDRI lighting, contact shadows, restrained post-processing. Bloom/DOF only if they serve the subject.
- Texture (paper, film grain, noise) should be subtle and static or very slow.

## 7. Hierarchy per scene
Each viewport answers, in order: **What is the subject? What is the one supporting fact? Where do I look next?**
Define primary / secondary / tertiary elements, the focal point, and the exit cue (scroll prompt, progress, leading line, object movement).

## 8. Subject-specific starting points
- **Product reveal:** hero object lighting, material close-ups, exploded/assembly, spec as visuals, one decisive CTA.
- **Scientific explainer:** scale ladders, cross-sections, labeled phases, controllable parameters, cited sources.
- **Industrial story:** process as journey (raw -> transform -> output), machinery scale, human presence, safety/impact data.
- **Data narrative:** one insight per scene, annotate the chart, transitions that preserve object identity between states.
- **Portfolio/brand:** the work is the hero; type and motion express personality; fast to content.
- **Redesign:** keep IA and content value; change composition language, type, rhythm, and motion first.

## 9. Anti-template list
Centered hero + 3 cards; purple-blue gradient; glass panels over blurred blobs; glow borders; every section fading up; emoji icons; stock handshake photos; uniform 24px rounded cards; sticky nav with identical pill button; "Features / Pricing / Testimonials" rhythm with no concept. Use any of these only with a stated reason. Note: glass chips over rich media, gradient display type, and dark grounds are legitimate when the selected style (S01/S03/O1 in `style-library.md`) calls for them; the problem is using them as a default with no concept.

See also `style-library.md` (26 styles), `style-selector.md` (automatic choice), and `taste-profile.md` (quality bar).
