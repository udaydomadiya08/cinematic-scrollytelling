# Taste Profile (the "motionsites-grade" quality bar)

This file captures the taste of the person who owns this skill, distilled from three
reference builds (see `source-prompts/`): a 3D-creator portfolio, a "Planet Jumping" portal
experience, and a scroll-scrubbed AI-company page. Apply it as the **default quality bar for
every build**, whichever style from `style-library.md` is selected. It describes *qualities*
to reach, not pages to copy.

## Contents
1. What the references have in common
2. The twelve taste rules
3. Signature moves worth reusing (technique level)
4. Things the references do NOT do
5. Copy-vs-craft boundary

## 1. What the references have in common
- **One big idea per first screen.** A monumental word, a window into another world, or a
  full-bleed film. Never a centered hero + three cards.
- **Media is the story.** Cinematic video, 3D renders, or a canvas effect carry the page;
  copy is short, uppercase or mono, and sits *on* the picture, not beside it.
- **Scroll or click *does* something to the picture.** Scrubbed video, a window that
  expands, cards that stack and shrink, text that fills in letter by letter, rows that
  slide opposite ways. The interaction is the content.
- **Heavy, confident geometry.** Huge type (14-22vw), very large radii (40-90px), pill
  buttons, full-bleed rounded sections that overlap the previous one.
- **Restraint in palette.** Near-black ground (#0A0A0A-#0C0C0C), one cool-silver gradient
  for display type, one saturated accent used once (the gradient CTA), or pure white sections
  for contrast inversion.
- **Premium polish in micro-detail.** Blur-in entrances, eased counters, magnetic hover,
  custom cursor with a label, staggered delays, drop-shadowed text over video.

## 2. The twelve taste rules
1. The first viewport has exactly one focal point and one memorable device.
2. Display type is oversized and *used as a design object* (gradient-filled, cropped by the
   viewport edge, overlapped by a subject, or masked with imagery).
3. Pair a heavy display face with a quiet text face; add mono only for labels/data.
4. Labels are small, uppercase, widely tracked (0.12-0.2em); body copy is light/regular and short.
5. Use **inversion** at least once: dark -> white (or white -> dark) with a rounded seam, so
   the page has a "chapter break" you can feel.
6. One section is a **moving-media moment** (marquee rows, scrubbed video, portal) and one is
   a **reading moment** (scroll-filled text, numbered list, fact table).
7. Numbers are big (01 / 02 / [03]) and used as navigation and rhythm, not decoration.
8. Every entrance is a blur + translate + fade with a stagger, on an expo-out/cubic curve
   (e.g. `cubic-bezier(.22,1,.36,1)` or `.16,1,.3,1`), 600-1100ms. No bounce.
9. One scroll-driven or pointer-driven signature interaction per page, executed fully.
10. Interface chrome is minimal: a pill nav, one CTA, a small index. It fades away during
    big transitions.
11. Clamp-based fluid type (`clamp()` / vw) so it scales from 375px to ultra-wide.
12. Everything degrades: poster, gradient, or procedural fallback when media fails;
    `prefers-reduced-motion` gives static, readable state.

## 3. Signature moves worth reusing (technique level)
| Move | Where to read the recipe |
|---|---|
| Gradient-filled giant type (`background-clip:text`, 180deg silver) | `technique-recipes.md` R15 |
| Subject (portrait/object) overlapping the giant type + magnetic follow | R6 |
| Two marquee rows moving opposite ways, driven by scroll offset | R4 |
| Paragraph that fills in letter-by-letter with scroll | R3 |
| Sticky cards that scale down as the next one stacks | R5 |
| Dark -> white inverted section with 40-60px rounded top seam | R15 |
| Scroll-scrubbed video through a canvas frame cache | R2 |
| Rounded "window" that tilts with the pointer then swallows the screen | R8 |
| Percentage preloader that hands off to a docked logo | R9 |
| Custom cursor (dot + lerped ring + contextual label) | R10 |
| Glass chips, left-accent badges, mono labels over video | R15 |

## 4. Things the references do NOT do
No parallax confetti, no emoji icons, no stock photography, no icon-card grids, no
neon-glow borders, no auto-playing carousels, no scroll hijacking of direction, no
paragraph-heavy sections. Media is full-bleed or heavily rounded, never boxed with a drop shadow.

## 5. Copy-vs-craft boundary
The three source prompts recreate existing sites. When building a **new** site, reuse the
*techniques, tokens and rhythm* but write original copy, choose original names, change the
palette/type to fit the subject, and never reuse the sample brand names, characters, or asset
URLs unless the user explicitly asks for an exact recreation. In recreation mode, follow
the matching file in `source-prompts/` literally.
