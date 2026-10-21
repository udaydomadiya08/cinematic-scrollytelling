# Technology and Performance Reference

## Contents
1. Stack selection
2. Repository-first rules
3. Rendering approach guide
4. Three.js / WebGL practices
5. Performance budgets and techniques
6. Accessibility
7. Responsive strategy
8. Resilience and cleanup
9. Dependency hygiene

## 1. Stack selection
Match the existing stack when there is one (Next.js, Vite, Astro, SvelteKit, plain HTML, etc.). For a new project, choose the smallest stack that works:
- Mostly static story + light motion: Astro or Vite + vanilla/TypeScript + CSS (+ GSAP if scroll choreography is complex).
- App-like or data-heavy interactivity: Next.js/Vite + React (+ R3F for 3D).
- Pure 3D showcase: Vite + Three.js (or R3F + drei) with a thin DOM layer.
Do not add libraries without a concrete need. Check versions and current docs of any library before writing API calls from memory.

## 2. Repository-first rules
Before editing: read `package.json`, lockfile, config, routing, global styles, existing components. Do not change framework, package manager, or folder conventions without reason. Do not overwrite existing files without reading them. Keep diffs focused; keep existing tests passing.

## 3. Rendering approach guide
| Need | Use |
|---|---|
| Layout, typography, controls | DOM/CSS |
| Diagrams, line art, path draw, masks | SVG |
| Particles, 2D data art, image sequence | Canvas 2D |
| Real-time spatial interaction, materials, camera | WebGL/Three.js |
| Fixed cinematic shot needing top fidelity | Video / image sequence |
| Mixed | Hybrid, one clear role per layer |

## 4. Three.js / WebGL practices
- One renderer, one animation loop; pause when off-screen (`IntersectionObserver`) or tab hidden.
- Cap `devicePixelRatio` (e.g., `Math.min(devicePixelRatio, 2)`, lower on mobile).
- Use `renderer.setAnimationLoop`; avoid per-frame allocations; reuse vectors/matrices.
- Color management: set output color space and tone mapping deliberately; check textures' color spaces.
- Load with GLTFLoader + Draco/meshopt/KTX2 loaders; show a loading state; handle load errors.
- Tie camera/object state to scroll progress through a single normalized value; damp smoothly.
- Post-processing: minimal, measured; disable on low-power devices.
- Detect WebGL failure and device capability; provide a static or 2D fallback.
- Dispose everything on teardown; remove listeners; cancel RAF.
- Test on a mid-range phone profile, not only a desktop GPU.

## 5. Performance budgets and techniques
Targets (verify, do not assume): LCP <= 2.5 s, INP <= 200 ms, CLS <= 0.1 on mid-range mobile over a throttled connection; sustained 60 fps on target devices for scroll scenes (at least stable 30 on low-end).
- Critical path first: hero visible and meaningful before heavy assets stream.
- Code-split heavy scenes; dynamic import 3D/GSAP plugins when first needed.
- Lazy-load below-the-fold media; preload only the true critical assets and fonts.
- Animate compositor-friendly properties; use `will-change` only on elements about to animate and remove after.
- Avoid scroll listeners that read layout each frame; batch reads/writes.
- Avoid large blur/backdrop-filter areas and many stacked filters.
- Use `content-visibility: auto` for long offscreen sections where safe.
- Prefer one video/canvas per viewport; pause others.
- Measure with Lighthouse/PageSpeed, browser Performance panel, and a real throttled run when possible. Report only what you measured.

## 6. Accessibility
- Semantic HTML landmarks and heading order, even in heavy scenes; visible focus styles; skip link.
- Keyboard-operable interactions; touch and pointer parity; targets >= 44x44 CSS px on touch.
- Text alternatives for meaningful images/diagrams (`alt`, `aria-label`, or adjacent description); decorative media `aria-hidden`.
- Canvas/WebGL content that carries meaning needs a text equivalent.
- `prefers-reduced-motion`, `prefers-color-scheme` (if offering both), `prefers-reduced-data` (where supported) considered.
- Do not rely on color alone; check contrast.
- Live-region or focus management for dynamic state changes triggered by interaction.

## 7. Responsive strategy
- Design mobile and desktop compositions separately; use container queries and `clamp()`.
- `svh`/`dvh` units for full-height sections; handle mobile browser chrome resize without retriggering expensive reflow.
- Lower scene lengths, simplify pins, reduce particle counts and texture sizes on small/low-power devices.
- Test landscape phones and large (1920+) and ultra-wide screens for composition breakage.
- Touch: replace hover-only effects with tap/drag alternatives.

## 8. Resilience and cleanup
- Every async asset load has loading, success, and error states.
- Clean up timelines, ScrollTriggers, observers, event listeners, RAF loops, GPU resources on unmount/route change.
- Guard against double-initialization (React strict mode, HMR).
- Handle offline/slow-network: poster images, retry, graceful degradation.
- Keep content readable with JS disabled where feasible for content sites (progressive enhancement); at minimum avoid a blank page.

## 9. Dependency hygiene
Pin versions via lockfile; avoid abandoned packages; check licenses of libraries (GSAP's current license terms, Three.js MIT, etc. - read the actual current terms before commercial use); run `npm audit` or equivalent when installing; do not claim compatibility you did not test.
