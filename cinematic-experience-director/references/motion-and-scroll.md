# Motion and Scrollytelling Reference

## Contents
1. Motion language
2. Easing and timing
3. Technique vocabulary
4. Scrollytelling mechanics
5. Pinning, scrubbing, snapping
6. Smooth scroll caution
7. Interruption, reversal, fast scroll
8. Reduced motion
9. Implementation patterns (GSAP-style)
10. Common failures

## 1. Motion language (define before animating)
- **Easings (2-3):** e.g. entrance `cubic-bezier(0.16, 1, 0.3, 1)` (expo-out), state change `cubic-bezier(0.65, 0, 0.35, 1)` (in-out), linear only for scrubbed/looping values.
- **Durations:** micro 120-200ms, UI 250-400ms, scene element 600-900ms, hero/signature 1000-1600ms.
- **Stagger:** 40-90ms between siblings; cap total stagger under ~600ms.
- **Distance/scale:** small offsets (8-24px) for UI, large travel (vh-scale) only for deliberate camera-like moves.
- **Signature transition:** one recurring transition that belongs to this project (wipe, iris, depth push, type-mask).
Write these down (in a comment block or `motion.ts`) and reuse them.

## 2. Easing and timing guidance
- Things entering or responding to the user: ease-out (fast start, soft land). Things leaving: ease-in, shorter. Moving on screen: ease-in-out.
- Scrub-linked motion: linear or very light smoothing so it tracks the scroll predictably.
- Prefer shorter than you think; if a user waits for an animation to finish, it is too long.
- Frequent interactions (hover, toggles) are near-instant; rare cinematic moments earn length.
- Animate `transform`, `opacity`, `clip-path`, `filter` (sparingly). Avoid animating layout properties (`width`, `height`, `top`, `left`, margins).

## 3. Technique vocabulary
Kinetic typography and masked line reveals; scroll-linked camera moves; layered parallax with real depth ratios; object assembly/disassembly; clip-path and mask wipes; SVG path drawing; animated diagrams and data flow; progressive construction/transformation; shared-element/object-constancy transitions; image-sequence scrubbing; shader-driven transitions; cursor/pointer-reactive lighting; particles/atmosphere (subtle); timeline-driven global states (e.g., `data-scene` attribute drives CSS variables); magnetic/inertial UI feedback; scroll-scrubbed video via canvas frame cache; pointer-tilted canvas "portal" windows that expand to full screen; letter-by-letter scroll-filled text; opposite-direction scroll marquees; sticky card stacking with scale-down; velocity-skewed type; horizontal scroll via sticky stage; blur-in staggered reveals. Working code for these is in `technique-recipes.md`.
Pick by purpose: **explain, orient, reward, connect, pace.** If a technique does none, cut it.

## 4. Scrollytelling mechanics
- Model the page as a **master timeline** of scenes. Each scene has a scroll range, local progress 0-1, and enter/active/exit states.
- Drive visuals from progress values, not from ad-hoc offsets. One source of truth per scene.
- Keep text readable at every progress value; never let essential copy exist only mid-animation.
- Provide orientation: progress indicator, scene labels, or anchors.
- Scene length budget: stillness scenes ~100vh; scrubbed sequences 200-500vh; avoid >600vh without payoff.

## 5. Pinning, scrubbing, snapping
- Pin only when sustained attention on one visual benefits the story.
- Use `pinSpacing` correctly and test content below pinned scenes.
- Scrub with small smoothing (e.g., 0.3-1) rather than heavy lag.
- Snap only for discrete states, with generous duration and `ease`; never fight the user's scroll direction.
- Avoid nested pins unless proven stable.

## 6. Smooth scroll caution
Libraries such as Lenis smooth wheel input and can improve scrubbed feel, but they can break native behaviors (anchor links, find-in-page, accessibility tools, overscroll, iOS momentum). Use only if the experience needs it, keep native scroll on touch unless tested, expose `scrollTo` for anchors, and disable when `prefers-reduced-motion` is set. Never hijack scroll direction or speed in a way that fights the user.

## 7. Interruption, reversal, fast scroll
- Every scrubbed animation must be reversible by construction.
- Time-based entrances should be `toggleActions: "play none none reverse"` or one-shot by choice; decide consciously.
- Test: scroll rapidly to the bottom and back; jump via anchor mid-scene; refresh mid-page (state restoration); resize/orientation change (`ScrollTrigger.refresh()` or equivalent); tab hidden and returned.
- Interrupting a transition should retarget from the current value, not snap or restart (CSS transitions do this; for JS use tweens with `overwrite: "auto"`).

## 8. Reduced motion
- Honor `prefers-reduced-motion: reduce`: remove parallax, autoplay loops, large translations, scroll-jacking, and flashing; replace with instant state changes or simple opacity.
- Content, navigation, and meaning must remain intact.
- Provide a manual pause for any autoplaying video/loop longer than 5 seconds.
- No flashing more than 3 times per second.

## 9. Implementation patterns (GSAP + ScrollTrigger style; adapt to the chosen stack)
```js
// Respect user preference and scope cleanup
const mm = gsap.matchMedia();
mm.add({
  motion: "(prefers-reduced-motion: no-preference)",
  reduce: "(prefers-reduced-motion: reduce)",
  desktop: "(min-width: 900px)",
}, (ctx) => {
  const { motion, desktop } = ctx.conditions;
  if (!motion) { /* set final states, no scrub */ return; }
  gsap.timeline({
    scrollTrigger: { trigger: ".scene-1", start: "top top", end: "+=250%", scrub: 0.5, pin: desktop },
  }).to(".hero-object", { scale: 1.4, yPercent: -10, ease: "none" })
    .to(".headline", { clipPath: "inset(0 0 0 0)", ease: "power3.out" }, "<0.1");
});
// React: wrap in useGSAP / gsap.context and revert on unmount.
```
Other rules: register plugins once; kill triggers on unmount; avoid creating triggers inside render; use `invalidateOnRefresh` when sizes drive values; use `100svh`/`dvh` rather than `100vh` on mobile; set explicit image dimensions so triggers measure correctly; call refresh after fonts/images load. Check the installed library version's docs before using API calls from memory.
CSS-only options (scroll-driven animations via `animation-timeline`) can replace JS for simple reveals where browser support meets the target; feature-detect with `@supports` and provide a fallback.

## 10. Common failures
Reveal triggers firing before layout settles; pinned scene jumps after fonts load; text unreadable during crossfades; parallax causing jitter on mobile; animations continuing off-screen; listeners and tickers never cleaned; scroll-linked work done in `scroll` handlers instead of rAF/ScrollTrigger; mouse-only interactions with no touch/keyboard equivalent.
