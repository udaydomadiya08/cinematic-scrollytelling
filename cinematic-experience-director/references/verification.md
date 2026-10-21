# Verification Reference

## Contents
1. Principle
2. Tooling
3. The loop
4. Viewport matrix
5. Visual critique rubric
6. Interaction and robustness tests
7. Automated checks
8. Evidence and reporting rules

## 1. Principle
Do not claim a browser test, screenshot, performance measurement, or behavior unless you actually observed or executed it. "It compiles" and "it should work" are not verification.

## 2. Tooling
Check what exists: Playwright, Puppeteer, Chrome DevTools MCP, Cypress, a browser-automation skill, or a plain headless Chromium. If Playwright is available: start the dev/prod server, drive the page, capture screenshots, scroll in steps, record console errors. If no browser tooling is available, say so, do static review (lint/types/build/code reading), and clearly mark visual claims as unverified.

## 3. The loop
1. Implement the intended experience.
2. Run it (dev or production preview).
3. Capture actual output at the viewport matrix, at several scroll positions per scene (start / mid / end of each scrubbed range).
4. Critique with the rubric below.
5. Fix the highest-impact defects in one focused batch (not whack-a-mole).
6. Re-capture and compare. Run checks. Stop when criteria are met; do not polish forever.

## 4. Viewport matrix
Minimum: 390x844 (phone), 768x1024 (tablet), 1440x900 (laptop). Add when relevant: 1920x1080, 2560x1080 ultra-wide, 844x390 landscape phone. Test both light/dark if offered, and reduced motion on/off.

## 5. Visual critique rubric (score each: strong / ok / weak; fix weak)
- **Hierarchy:** one clear focal point; supporting info subordinate.
- **Composition:** deliberate use of space, crop, scale; not a template.
- **Typography:** readable size, contrast, measure, no orphan/overflow; no layout shift on font load.
- **Imagery:** sharp, cohesive grade and lighting; no pixelation, artifacts, mismatched perspective.
- **Motion:** purposeful, smooth, not repetitive; no jank, stutter, or snapping; hierarchy of what moves.
- **Story:** can a stranger state the message from visuals alone?
- **Transitions:** scene entry/exit are continuous, no blank frames or flashes.
- **Mobile:** composition reworked, not merely squeezed; thumb reachable controls.
- **Distinctiveness:** would this be mistaken for a generic template?

## 6. Interaction and robustness tests
- Scroll forward, reverse, fast, jump by anchor, refresh mid-page, resize, rotate.
- Rapid repeated interaction (spam toggles/clicks/drags).
- Keyboard-only navigation: tab order, focus visibility, Escape/Enter/arrow behavior.
- Touch: swipe, pinch where relevant, no scroll traps.
- Block or delay assets: verify loading state and error fallback.
- Disable WebGL (or emulate) and verify fallback.
- Reduced motion: verify static final states and complete content.
- Slow network and CPU throttle for one pass.
- Console: no errors or uncaught promise rejections; no memory growth when navigating/re-entering scenes (spot check).

## 7. Automated checks (run what exists in the repo)
Production build; lint; type check; unit/e2e tests if present; optionally Lighthouse and an accessibility scan (axe or similar). Record pass/fail and any skipped checks with reasons.

## 8. Evidence and reporting rules
- Report: what you ran, viewports tested, issues found and fixed, remaining known issues.
- Distinguish **observed** from **inferred** from **not tested**.
- Include measured numbers only if actually measured, with conditions (device profile, throttle).
- Never describe a screenshot you did not capture or look at.
