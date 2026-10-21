# Style Library (26 scrollytelling / immersive styles)

Each style is a *direction*, not a template. The selector (`style-selector.md`) picks one
primary style (plus at most two secondary and one overlay). Then bend it to the subject using
`art-direction.md` and the taste bar in `taste-profile.md`. Recipes are in `technique-recipes.md`
(R1-R20). Entries marked **[REF]** have a literal reference prompt in `source-prompts/`.

## Contents
- S01 Monumental Gradient Type Portfolio [REF]
- S02 Portal / Destination Hop [REF]
- S03 Scroll-Scrubbed Film Background (+ glass UI) [REF]
- S04 Pinned Chapter Storytelling
- S05 Image-Sequence Product Reveal
- S06 3D Object Showcase / Exploded View (Three.js)
- S07 Layered Parallax Descent
- S08 Horizontal Scroll Gallery / Film Strip
- S09 Stacking Case-Study Cards
- S10 Type-as-Window / Mask Reveal
- S11 Kinetic Type Brutalist
- S12 Editorial Long-Read
- S13 Data Narrative (morphing charts)
- S14 Blueprint / Technical Instrument
- S15 Luxury Quiet
- S16 Retro-Future / Archival / Film Grain
- S17 Shader / Liquid Distortion
- S18 Zoom-Through / Scale Journey
- S19 Route / Map Journey
- S20 Timeline River
- S21 Bento Reveal Grid
- S22 Terminal / Cyber / Code
- S23 Playful Kinetic / Toy
- S24 Organic Documentary / Nature
- S25 Spotlight / Cursor-Lit Reveal
- S26 Interactive Explainer Lab
- Overlays O1-O4 (cross-cutting systems)

Entry format: **Best for / Feel / Signature / Look / Layout & motion / Build / No-asset fallback / Mobile / Avoid**

---

## S01 Monumental Gradient Type Portfolio [REF: 01]
- **Best for:** creators, designers, 3D artists, agencies, personal brands, studios, founders.
- **Feel:** confident, premium, dark, sculptural.
- **Signature:** the name/greeting is set at 14-18vw in a silver gradient and a cut-out subject
  (portrait, 3D object) overlaps it and follows the pointer magnetically.
- **Look:** ground #0C0C0C; type gradient 180deg #646973 -> #BBCCD7; text #D7E2EA; one accent
  gradient used only on the CTA pill; heavy sans (Kanit/Archivo/Familjen/Anton at 900) uppercase.
- **Layout & motion:** hero -> two-row scroll marquee of work previews (rows go opposite
  ways) -> "About" with 4 floating 3D icons + scroll-filled paragraph -> **white inverted
  Services** list with giant numerals and rounded-t-[60px] seam -> dark "Projects" with
  sticky stacking cards. See R3, R4, R5, R6, R15.
- **Build:** React+Tailwind+Framer Motion if a React repo/stack is requested; otherwise a single
  HTML file with vanilla JS recipes. 
- **No-asset fallback:** subject = CSS/SVG object or Three.js primitive with a soft material;
  marquee tiles = generated gradient+type cards.
- **Mobile:** heading at 14vw, portrait centered behind text, marquee tiles 260x170.
- **Avoid:** cloning the sample "Jack" copy or the exact asset URLs.

## S02 Portal / Destination Hop [REF: 02]
- **Best for:** space, travel, destinations, games, worlds, product "modes", cities, planets,
  seasons, anything with a small set of *places/states* the visitor hops between.
- **Feel:** cinematic, immersive, one-screen, tactile.
- **Signature:** a rounded "window" (radius ~90px) that tilts with the pointer; clicking it
  expands to swallow the screen while a transition film plays; the window re-opens on the next
  state. Giant condensed title bottom-left; facts table bottom-right.
- **Look:** near-black, white type, translucent pill nav, thin 1px white rules, condensed display
  face for the state title + a neutral grotesk for facts; blur-in entrances.
- **Layout & motion:** no page scroll; state machine (A -> B -> C); preloader with 0-100%
  counter -> logo flies to header; custom cursor labelled "Enter". See R8, R9, R10, R14.
- **Build:** single HTML + Canvas 2D (no libraries). Video optional.
- **No-asset fallback:** each state's "film" = a procedural canvas scene (starfield/nebula,
  gradient noise, orbiting shapes) - the mask mechanics are unchanged.
- **Mobile:** window top 44%, 66vw wide; chrome simplified; tap = enter.
- **Avoid:** more than ~5 states; letting video decode stall the transition (preload next).

## S03 Scroll-Scrubbed Film Background (+ glass UI) [REF: 03]
- **Best for:** AI/SaaS/tech companies, startups, fintech, studios, product launches, abstract
  concepts, anything with one striking looped 3D/AI film.
- **Feel:** sleek, atmospheric, editorial, quiet confidence.
- **Signature:** a full-viewport film is *scrubbed by scroll* (not autoplayed); sparse text blocks
  and glass chips float over it, revealed with staggered fade-up.
- **Look:** ground #0A0A0A; white type with drop-shadow; one sans (Inter/Geist/Switzer) + mono
  labels `10-11px uppercase tracking-[.15em]`; glass tokens from O1; hairline borders.
- **Layout & motion:** fixed video/canvas layer z-0; 2-4 full-height sections separated by
  an 80vh spacer so the film has room to scrub; top row = tiny labels + short intro; bottom row
  = giant headline + CTA / glass card. See R2, R7, R15.
- **Build:** React or single HTML. Frame cache (R2b) for smoothness; seek fallback (R2a).
- **No-asset fallback:** WebGL/Canvas generative film (flow-field, metaball, noise sphere)
  whose time parameter = scroll progress.
- **Mobile:** same; poster image first; reduce cached frames to ~48 at max 640px.
- **Avoid:** autoplay loop; opaque panels over the film; icon-card grids.

## S04 Pinned Chapter Storytelling
- **Best for:** startups explaining a product, process stories, non-profits, how-it-works,
  industrial, health, education, any 3-7 step narrative.
- **Feel:** guided, clear, confident.
- **Signature:** one sticky visual (diagram, device, scene) changes state as chapter text scrolls
  past; a rail of numbered chapters shows progress.
- **Look:** flexible - pick any archetype from `art-direction.md`; strong chapter numerals.
- **Layout & motion:** 2-column sticky stage + steps (R14); 100vh per step; visual morphs
  via CSS variables / `data-step`; progress rail.
- **Build:** HTML + IntersectionObserver (+ GSAP ScrollTrigger if pin/scrub needed).
- **No-asset fallback:** SVG diagram whose parts toggle per step.
- **Mobile:** visual pinned on top 45vh, text below, or visual inline per step.
- **Avoid:** more than 7 steps; text that only exists mid-animation.

## S05 Image-Sequence Product Reveal
- **Best for:** hardware, cars, bikes, watches, shoes, cameras, headphones, appliances.
- **Feel:** Apple-grade, tactile, glossy, object-centered.
- **Signature:** a product rotates/assembles/explodes as you scroll, drawn from 60-180 frames on
  a canvas; spec callouts appear at angle milestones.
- **Look:** studio lighting, one ground color matched to the frames, giant model name,
  restrained text, one CTA.
- **Layout & motion:** 300-500vh pinned canvas (R13), callouts keyed to progress ranges,
  final still + buy CTA.
- **Build:** canvas image sequence (WebP/AVIF frames, ~1280w) or video->frames via ffmpeg.
- **No-asset fallback:** Three.js model/primitive turntable (S06) or SVG exploded drawing.
- **Mobile:** fewer frames (every 2nd), 960w, lower DPR.
- **Avoid:** loading all frames before first paint; mismatched lighting between frames.

## S06 3D Object Showcase / Exploded View (Three.js)
- **Best for:** products, configurators, architecture models, science objects, game/NFT items.
- **Feel:** spatial, technical, interactive.
- **Signature:** the camera flies around/through a real-time 3D object; parts separate; materials
  swap; pointer orbit between scroll scenes.
- **Look:** neutral studio HDRI or dark void + rim light; labels in mono; thin leader lines.
- **Layout & motion:** fixed canvas + DOM text; scroll maps to camera path/timeline (R18).
- **Build:** Three.js (pinned CDN version) or R3F; GLB with Draco; lazy init; pause off-screen.
- **No-asset fallback:** built-from-primitives model (torus knots, lathe, extrude) with PBR materials.
- **Mobile:** lower pixel ratio (<=1.75), no post-processing, tap-to-orbit.
- **Avoid:** heavy post FX; unlit flat materials; no-WebGL dead end (provide poster).

## S07 Layered Parallax Descent
- **Best for:** nature, oceans, mountains, fantasy, travel, climate, origin/"depth" stories,
  atmosphere-to-core metaphors.
- **Feel:** vertical journey with real depth.
- **Signature:** 4-7 transparent layers move at different rates; the viewer descends through them
  (sky -> forest -> cave -> core) with fog and light shifts between strata.
- **Look:** painterly or photographic layers, one color grade, haze gradients, minimal type.
- **Layout & motion:** `transform: translate3d` with ratios 0.1-0.9; scene-level palette swap
  through CSS variables; depth labels ("0 m", "-200 m").
- **Build:** DOM layers + rAF scroll; SVG silhouettes if no art.
- **No-asset fallback:** layered SVG silhouettes with gradient fog and grain.
- **Mobile:** fewer layers (3-4), smaller offsets.
- **Avoid:** parallax with no depth logic (everything drifting randomly).

## S08 Horizontal Scroll Gallery / Film Strip
- **Best for:** photographers, architects, fashion lookbooks, real estate, portfolios, menus,
  collections, timelines of artwork.
- **Feel:** curated, gallery-like, rhythmic.
- **Signature:** vertical scroll drives a long horizontal strip with varied frame sizes;
  one frame expands to full screen as detail view.
- **Look:** large photos, small captions, index counter "03/12", quiet ground.
- **Layout & motion:** sticky stage + translateX (R11); parallax inside frames (image moves
  slower than frame); cursor "drag/view" label (R10).
- **Build:** HTML/CSS/JS.
- **No-asset fallback:** generated gradient/pattern frames labelled as placeholders.
- **Mobile:** native horizontal swipe with scroll-snap instead of scroll-jacking.
- **Avoid:** equal-size frames; strip longer than ~600vh of scroll.

## S09 Stacking Case-Study Cards
- **Best for:** agencies, freelancers, product studios, startups with multiple products, services.
- **Feel:** organized, tactile, confident.
- **Signature:** each project card sticks at the top and scales/dims as the next slides over it;
  each card contains a bento of 3 images + big number + category + CTA.
- **Look:** very large radius (40-60px), 2px light borders on dark, huge numerals.
- **Layout & motion:** R5; `top` offset per card (index * 28px); scale target = 1 - (n-1-i)*0.03.
- **Build:** CSS sticky + scroll listener; or Framer Motion `useScroll/useTransform`.
- **No-asset fallback:** gradient/pattern or SVG mock covers.
- **Mobile:** drop to 85vh cards, keep stacking.
- **Avoid:** >5 cards; covering the CTA.

## S10 Type-as-Window / Mask Reveal
- **Best for:** film, sports, fashion, music, events, brands with a bold name, sneaker drops.
- **Feel:** loud, graphic, cinematic.
- **Signature:** giant letters act as a window; video/image plays inside the glyphs, or the type
  scales up until the viewer "falls through" an O into the next scene.
- **Look:** 1-2 colors, heavy grotesk or condensed face at 25-40vw, high contrast.
- **Layout & motion:** `mix-blend-mode`, `background-clip:text` over video, or SVG `<mask>`/clip-path
  scaled with scroll (R12).
- **Build:** HTML+SVG; video poster fallback.
- **No-asset fallback:** animated gradient/noise canvas inside the glyphs.
- **Mobile:** 2-3 big letters instead of full words; vertical stack.
- **Avoid:** thin fonts (no window), low-contrast fills, long words.

## S11 Kinetic Type Brutalist
- **Best for:** agencies, music, youth brands, events, fashion, zines, culture, startups with edge.
- **Feel:** raw, loud, fast, anti-polish (but still rigorous).
- **Signature:** infinite marquees, rotating/stretching text, hard cuts, outlines, stickers, grid
  lines; type is both layout and animation.
- **Look:** flat colors (acid green, red, cobalt, off-white), black 2-4px borders, mono + wide grotesk.
- **Layout & motion:** velocity-linked marquee skew (speed = scroll velocity), word-swap loops, hover
  inversions; snap cuts between sections.
- **Build:** CSS + tiny JS.
- **No-asset fallback:** native (it is type-only).
- **Mobile:** same, slower speeds.
- **Avoid:** illegible long copy; seizure-risk flicker (<3 flashes/s).

## S12 Editorial Long-Read
- **Best for:** journalism, essays, research, non-profit reports, books, interviews, culture, history.
- **Feel:** human, literary, trustworthy.
- **Signature:** a magazine-grade reading experience with pull-quotes, drop caps, sidenotes, full-bleed
  photographs, and a few well-timed motion moments (image reveal, number count).
- **Look:** serif display + readable text serif/sans; paper or deep ink ground; hairline rules.
- **Layout & motion:** 12-col asymmetry; sticky marginalia; image masks reveal on enter; reading
  progress bar.
- **Build:** HTML/CSS; light JS.
- **No-asset fallback:** typographic cover + SVG illustrations + pull-quote art.
- **Mobile:** single column; keep marginalia as inline notes.
- **Avoid:** over-animating text people read.

## S13 Data Narrative (morphing charts)
- **Best for:** reports, climate, finance, health stats, elections, sports analytics, ESG, research.
- **Feel:** clear, authoritative, discoverable.
- **Signature:** one chart object persists and *morphs* between insights (bars -> map -> line) as
  the story advances; annotations pop on the relevant mark.
- **Look:** calm palette, one highlight color, labelled units, big numerals.
- **Layout & motion:** sticky chart + narrative steps (R14); transitions preserve object identity.
- **Build:** D3/SVG or Canvas; pin library versions.
- **No-asset fallback:** native; use real or clearly-labelled illustrative data.
- **Mobile:** chart on top, steps below; larger touch targets.
- **Avoid:** unlabeled axes; decorative 3D charts; fake data presented as real.

## S14 Blueprint / Technical Instrument
- **Best for:** engineering, industrial, robotics, cybersecurity, fintech infra, B2B, devices, labs.
- **Feel:** precise, trustworthy, instrument-grade.
- **Signature:** a technical drawing that draws itself and is annotated with mono callouts, scale bars
  and live-looking readouts.
- **Look:** blueprint blue or graphite/white; 1px lines, grid, mono labels, tabular numerals.
- **Layout & motion:** SVG path draw (R17), callout lines with leader dots, hover reveals specs.
- **Build:** SVG + JS.
- **No-asset fallback:** native.
- **Mobile:** crop diagram to the part of interest; stack callouts.
- **Avoid:** fake precision; unreadable tiny labels.

## S15 Luxury Quiet
- **Best for:** jewelry, watches, perfume, high-end hospitality, architecture, wellness, wedding.
- **Feel:** calm, expensive, slow.
- **Signature:** one hero object or place with generous negative space; slow easing; subtle light
  sweep; almost no UI.
- **Look:** warm neutrals or deep black + champagne; high-contrast serif or very fine grotesk;
  small caps labels.
- **Layout & motion:** 1-2 big moves per scene, 1.2-1.8s eases, soft parallax, cross-fades.
- **Build:** HTML/CSS (+ video or image sequence).
- **No-asset fallback:** photographic stand-in is the hard part - use SVG/CSS light studies.
- **Mobile:** same silence; larger type.
- **Avoid:** loud CTAs, badges, discount language.

## S16 Retro-Future / Archival / Film Grain
- **Best for:** history, film, music, books, vintage brands, anniversaries, museums, games.
- **Feel:** tactile, nostalgic, annotated.
- **Signature:** a scrapbook/archive world - paper, tape, CRT/scanlines, film burn, stamped dates -
  assembled as you scroll.
- **Look:** period type, limited inks (cream, red, black), grain overlay, halftone.
- **Layout & motion:** elements land like prints; sprocket or timecode HUD; flicker only subtly.
- **Build:** CSS filters, SVG noise, small JS.
- **No-asset fallback:** native.
- **Mobile:** simplify overlays.
- **Avoid:** pastiche without a point; heavy grain that hurts legibility.

## S17 Shader / Liquid Distortion
- **Best for:** creative studios, fashion, music, art, crypto/web3 culture, experimental portfolios.
- **Feel:** fluid, tactile, experimental.
- **Signature:** images ripple/melt/RGB-split on hover and scroll velocity via a WebGL fragment shader.
- **Look:** big imagery, minimal type, dark or saturated ground.
- **Layout & motion:** plane per image with uniform `uVelocity`, `uHover`; smooth scroll optional.
- **Build:** raw WebGL or Three.js plane meshes.
- **No-asset fallback:** procedural gradient textures.
- **Mobile:** reduce effect, drop to CSS filters if GPU is weak.
- **Avoid:** shader noise that hurts readability; no fallback without WebGL.

## S18 Zoom-Through / Scale Journey
- **Best for:** science, biology, astronomy, nanotech, economics, maps, "powers of ten" concepts.
- **Feel:** awe, continuity, scale.
- **Signature:** one continuous zoom: each scene is the previous scene's interior; scale labels tick
  (1 m -> 1 mm -> 1 um...).
- **Look:** scene palettes shift with scale; HUD scale bar; minimal text.
- **Layout & motion:** nested scenes scaled by `scroll^k`; crossfade at thresholds; labeled units.
- **Build:** CSS transforms / canvas; Three.js camera dolly for 3D.
- **No-asset fallback:** SVG/canvas concentric scenes.
- **Mobile:** fewer scales; vertical HUD.
- **Avoid:** scale jumps with no continuity cue; invented scientific claims.

## S19 Route / Map Journey
- **Best for:** travel, tourism, expeditions, logistics, migration, history campaigns, tours.
- **Feel:** adventurous, orienting.
- **Signature:** a line draws along a stylized map as the camera follows; stops pop with photo cards.
- **Look:** custom cartography (flat color regions, thin coast lines), compass/coordinates, serif labels.
- **Layout & motion:** SVG path + `getPointAtLength` (R17); pinned map; stop cards per chapter.
- **Build:** SVG (or MapLibre if real maps are needed).
- **No-asset fallback:** hand-built SVG map of the real geography you can verify; else abstract map.
- **Mobile:** map top, cards bottom.
- **Avoid:** inaccurate geography; unlabeled routes.

## S20 Timeline River
- **Best for:** company history, product evolution, biographies, museums, campaigns, roadmaps.
- **Feel:** flowing, chronological.
- **Signature:** a vertical or horizontal "river" line with eras as banks; each era changes the
  palette/type slightly.
- **Look:** year numerals as architecture, era palettes, small artifact images.
- **Layout & motion:** sticky year indicator, line draw, era color shift via `data-era`.
- **Build:** HTML/CSS/JS.
- **No-asset fallback:** typographic eras.
- **Mobile:** single-column timeline.
- **Avoid:** equal-weight events; invented dates.

## S21 Bento Reveal Grid
- **Best for:** feature overviews for apps/SaaS/hardware, dashboards, "what's new" releases.
- **Feel:** modular, tidy, product-y.
- **Signature:** a grid of unequal tiles that assemble on scroll, each tile containing a *live* mini
  demo (not an icon).
- **Look:** big radii, subtle inner borders, one hero tile.
- **Layout & motion:** staggered tile entrance; tile hover depth; one tile = animated demo.
- **Build:** CSS Grid + small JS.
- **No-asset fallback:** CSS/SVG mini demos.
- **Mobile:** 1-2 columns, hero tile first.
- **Avoid:** identical icon+title+blurb tiles.

## S22 Terminal / Cyber / Code
- **Best for:** developer tools, cybersecurity, hacking/CTF, AI infra, open source, games.
- **Feel:** technical, kinetic, insider.
- **Signature:** scroll types, runs, and resolves a believable terminal/CRT session that explains the product.
- **Look:** near-black, phosphor or amber accent, mono type, scanlines (subtle).
- **Layout & motion:** command lines typed by scroll progress; output blocks reveal; glitch only on
  transitions.
- **Build:** HTML/CSS/JS.
- **No-asset fallback:** native.
- **Mobile:** smaller font, horizontal scroll for wide lines avoided via wrapping.
- **Avoid:** cliche green-rain with no content; unreadable contrast.

## S23 Playful Kinetic / Toy
- **Best for:** kids, education, consumer apps, food, games, community brands.
- **Feel:** bouncy, friendly, tactile.
- **Signature:** draggable/physics objects, sticker pile, character that reacts to scroll.
- **Look:** saturated palette, chunky rounded type, thick outlines, big shadows.
- **Layout & motion:** springs (use sparingly but meaningfully), squash-stretch, hover wiggle.
- **Build:** CSS + JS (Matter.js optional).
- **No-asset fallback:** SVG characters/shapes.
- **Mobile:** touch drag; fewer bodies.
- **Avoid:** childish when the audience is professional.

## S24 Organic Documentary / Nature
- **Best for:** food, farms, coffee, wildlife, environment, travel, outdoor brands, wellness, NGOs.
- **Feel:** warm, human, textured.
- **Signature:** full-bleed photography/video with captions, ambient sound toggle, slow Ken-Burns,
  and a map/season marker.
- **Look:** earthy or dawn palettes, humanist serif + sans, grain, natural light.
- **Layout & motion:** alternating full-bleed + text, slow fades, parallax stills, mute-by-default audio.
- **Build:** HTML/CSS with lazy video.
- **No-asset fallback:** photographic gap is real - state placeholders and use textured gradients.
- **Mobile:** vertical crops; reduce video.
- **Avoid:** stock-looking imagery; autoplay audio.

## S25 Spotlight / Cursor-Lit Reveal
- **Best for:** mysteries, horror/noir, security, museums, escape rooms, "hidden layer" stories.
- **Feel:** curious, discovery-driven.
- **Signature:** a flashlight/lens follows the cursor/finger and reveals the hidden layer beneath.
- **Look:** dark ground + one revealed palette, grain, vignette.
- **Layout & motion:** radial mask via CSS variables `--x/--y`; scroll switches layers.
- **Build:** CSS mask + JS pointer.
- **No-asset fallback:** native.
- **Mobile:** auto-sweeping light path + tap/drag.
- **Avoid:** hiding essential content behind hover only.

## S26 Interactive Explainer Lab
- **Best for:** science, math, finance, medicine, engineering, "how it works" learning.
- **Feel:** curious, hands-on, rigorous.
- **Signature:** sliders/toggles directly change a live model; scroll introduces one variable at a time.
- **Look:** calm lab palette, labeled units, plot + controls panel.
- **Layout & motion:** scrollytelling steps unlock controls; results update instantly; reset button.
- **Build:** HTML + Canvas/SVG; read `explainers-and-data.md`.
- **No-asset fallback:** native.
- **Mobile:** controls docked bottom.
- **Avoid:** presenting a toy model as validated simulation (label "illustrative").

---

## Overlays (cross-cutting systems; combine with any style)
- **O1 Glass/Chip System** - `bg-white/10-15 + backdrop-blur-md + border-white/15-25`; left-accent mono badges;
  text drop-shadows over media. Use only over rich media, never over flat ground.
- **O2 Preloader + Docked Logo** - counter 0-100 tied to real asset progress, logo flies to header (R9).
- **O3 Custom Cursor** - dot + lerped ring + contextual label (R10); disabled on touch.
- **O4 Chapter Rail** - numbered index `01 02 03` or planet-list sidebar that tracks the active scene.
