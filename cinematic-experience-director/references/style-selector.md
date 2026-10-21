# Style Selector (automatic best-fit style choice)

Goal: when the user gives only a topic ("make a scrollytelling site for a coffee roaster",
"website about black holes", "portfolio for a 3D artist") or a topic plus loose instructions,
choose the best-fitting style from `style-library.md` **without asking**, justify it in five lines,
then build it.

## Contents
1. Inputs to read
2. Procedure (7 steps)
3. Keyword triggers (explicit style requests)
4. Topic -> style table
5. Scoring grid for ambiguous cases
6. Combination rules
7. Variety rule
8. Style Decision Record (what to show the user)
9. Switching styles on request

## 1. Inputs to read
Extract from the request, inferring what is missing: **topic**, **audience**, **goal** (sell,
explain, impress, inform, recruit, donate), **mood words**, **explicit style/reference words**,
**assets supplied** (video, images, 3D, brand), **page type** (one page, portfolio, product, story),
**device/performance constraints**, **requested intensity 1-5** (default 4), **stack** (default below).

## 2. Procedure
1. **Explicit beats inferred.** If the user names a style, site, effect, or pastes a reference
   (see section 3), use it as primary. Still choose secondaries by fit.
2. **Classify the subject's nature**: Object (product) / Place or world / Process or system /
   Data or evidence / Person or brand / Idea or emotion / Collection of work.
3. **Look up the topic table** (section 4) to get a *shortlist of 2-3 styles*.
4. **Check assets reality.** What can truly be obtained or generated? No film -> avoid S03
   film mode unless a procedural film is built. No frames -> avoid S05 or build with Three.js.
   No photos -> avoid S24/S08. Use each style's *No-asset fallback*.
5. **Score the shortlist** with the grid (section 5) when it is not obvious.
6. **Pick 1 primary + 0-2 secondary + 0-1 overlays** (section 6).
7. **Write the Style Decision Record** (section 8), then proceed to Phase 3 art direction.
   Do not stall with questions; at most one bundled question if a missing fact truly blocks
   the result (e.g. a real brand name or required language).

## 3. Keyword triggers (explicit style requests)
| If the user says / pastes | Use |
|---|---|
| "portfolio", "giant name", "gradient text", "3D creator", "marquee of work", "stacking cards" | S01 (+S09) |
| "portal", "planet", "destination", "click to travel", "window expands", "hop between" | S02 |
| "scroll video", "video scrubs on scroll", "AI landing page with video", "motionsites" | S03 |
| "pin", "sticky", "step by step", "chapters", "how it works" | S04 |
| "Apple-style", "product rotates on scroll", "frame sequence" | S05 |
| "3D", "Three.js", "WebGL object", "exploded view", "configurator" | S06 |
| "parallax", "descend", "depth", "layers" | S07 |
| "horizontal scroll", "gallery", "lookbook", "film strip" | S08 |
| "case studies", "work cards", "stacked projects" | S09 |
| "text mask", "video inside text", "big letters window" | S10 |
| "brutalist", "kinetic type", "loud", "marquee text", "zine" | S11 |
| "magazine", "long-read", "essay", "editorial" | S12 |
| "charts", "data story", "stats", "report" | S13 |
| "blueprint", "technical", "engineering", "schematic" | S14 |
| "luxury", "minimal", "elegant", "quiet" | S15 |
| "retro", "vintage", "archive", "film grain", "80s/90s" | S16 |
| "shader", "liquid", "distortion", "ripple" | S17 |
| "zoom", "scale", "powers of ten", "microscope to cosmos" | S18 |
| "route", "map", "journey", "trip" | S19 |
| "timeline", "history", "evolution" | S20 |
| "bento", "feature grid" | S21 |
| "terminal", "hacker", "cyber", "developer tool" | S22 |
| "playful", "kids", "toy", "fun" | S23 |
| "documentary", "nature", "farm", "wildlife" | S24 |
| "flashlight", "spotlight", "reveal under cursor" | S25 |
| "simulation", "interactive lab", "sliders" | S26 |
If the user asks for "all kinds"/"surprise me", pick by topic and mention two alternates.

## 4. Topic -> style table (primary / good secondaries / avoid)
| Topic family | Primary | Secondary options | Avoid |
|---|---|---|---|
| Space, planets, astronomy, sci-fi worlds | S02 or S18 | S03, S07, O2, O3 | S12 light-paper looks |
| AI / SaaS / startup / tech company | S03 | S04, S21, O1 | S16, S23 |
| Developer tool / cyber / infra / web3 | S22 | S14, S17, S03 | S15, S23 |
| 3D artist / designer / creative portfolio | S01 | S09, S17, S08, O3 | S12 |
| Agency / studio / creative collective | S11 or S09 | S10, S17, S01 | S15 |
| Photographer / filmmaker / visual artist | S08 | S17, S24, S25 | S21 |
| Automotive / motorbike / EV | S05 | S06, S10, S04 | S23 |
| Consumer hardware / gadget / audio / camera | S05 or S06 | S21, S04 | S16 |
| Luxury / watch / jewelry / perfume / hotel / wedding | S15 | S05, S24, S12 | S11, S23 |
| Fashion / streetwear / sneakers | S10 or S08 | S11, S17, S05 | S14 |
| Music / festival / event / nightlife | S11 or S17 | S10, S03, S16 | S12 |
| Film / TV / game launch | S10 or S02 | S03, S16, S25 | S21 |
| Gaming / esports | S22 or S02 | S10, S23 | S12 |
| Food / restaurant / coffee / farm | S24 | S15, S08, S23 | S14 |
| Travel / destination / tourism / expedition | S19 or S07 | S24, S08, S02 | S22 |
| History / museum / heritage / biography | S20 | S16, S12, S18 | S22 |
| Science / biology / physics / chemistry | S18 or S26 | S13, S04, S14 | S11 |
| Medical / health / wellness | S26 or S04 | S15, S24, S13 | S11, S22 |
| Climate / environment / ocean / wildlife | S07 or S24 | S13, S18, S19 | S22 |
| News / journalism / research report / policy | S12 or S13 | S20, S04 | S10, S17 |
| Finance / fintech / economics | S13 or S14 | S03, S15, S04 | S23 |
| Industrial / manufacturing / energy / logistics | S04 or S14 | S19, S18, S13 | S23 |
| Architecture / real estate / interior | S08 or S07 | S15, S06, S19 | S11 |
| Education / kids / learning | S23 or S26 | S04, S20 | S22 |
| Non-profit / campaign / social cause | S12 or S04 | S24, S13, S20 | S17 |
| Book / author / literature | S12 or S16 | S15, S20 | S21 |
| Personal CV / resume / founder page | S01 or S04 | S09, S21 | S11 unless edgy |
| Event invite / wedding / birthday | S15 or S23 | S24, S16 | S14 |
| Mystery / horror / noir / true-crime | S25 | S16, S12 | S23 |
| Unclear / generic business | S04 | S03 or S21, O4 | S11, S17 |

## 5. Scoring grid (use when two or more styles tie)
Score 0-2 on each; highest total wins; ties -> the one with the better no-asset fallback.
| Axis | Question |
|---|---|
| Subject fit | Does the style's signature *mean something* for this subject? |
| Emotion fit | Does the style produce the desired feeling? |
| Asset realism | Can we build it well with what exists or can be generated? |
| Info density | Can the style carry the amount of content required? |
| Device/perf | Will it hold on mid-range phones and in an iframe/artifact? |
| Distinctiveness | Will the result look different from the last site we built? |
Penalty -1 if the style would need a library or media we cannot verify.

## 6. Combination rules
- **One primary** owns the hero and the signature interaction.
- **Up to two secondaries**, each limited to a *specific scene* (e.g. S09 for the projects section,
  S13 for one stats scene).
- **Up to one overlay** from O1-O4 per chrome layer; O3 cursor and O2 preloader are optional
  polish, not requirements.
- Never combine two primaries (e.g. S02 + S05) - the page would have two competing signatures.
- Maintain one palette, one type system, one motion language across all scenes.

## 7. Variety rule
If asked for several sites in one conversation, or the same topic twice, change primary style,
archetype, palette family and type pairing each time. If outputs begin to look alike, the selection
step was skipped.

## 8. Style Decision Record (show before building; max ~8 lines)
```
Style decision
- Topic read as: <subject nature> for <audience>, goal <goal>
- Primary: S## <name> - because <1 line>
- Secondary: S## (scene) / S## (scene)   Overlay: O#
- Signature idea: <one sentence>
- Asset plan: <real | generated | procedural fallback>
- Stack: <single HTML | React+Vite | existing repo>   Intensity: n/5
- Alternates (say "switch to S##"): S##, S##
```

## 9. Switching styles on request
If the user says "switch to S##" or "make it more <mood>", keep content/IA, change composition
language, type, palette, and motion; do not just recolor. Record the new decision.

## Default stack (when the user and repo do not specify)
Single self-contained HTML file with inline CSS/JS; CDN libraries only when needed and pinned to exact
versions (GSAP/ScrollTrigger, Three.js); React + Vite + Tailwind + Framer Motion when the user asks
for React/TypeScript or a repo already uses it. Always provide poster/gradient fallbacks for remote media.
