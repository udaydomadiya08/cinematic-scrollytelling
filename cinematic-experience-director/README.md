# cinematic-experience-director

A reusable AI coding skill that turns ambitious ideas into distinctive, motion-rich, technically sound, browser-verified web experiences: cinematic scrollytelling, product reveals, scientific/industrial explainers, data narratives, 3D showcases, and redesigns.

## What is new in this version
- **Automatic style engine:** give a topic and the skill picks the best-fit style from 26 (plus 4 overlays), shows a short decision record, then builds.
- **Taste profile** distilled from three reference builds (3D portfolio, portal experience, scroll-scrubbed film page).
- **Technique recipes** (R1-R20): tested-syntax vanilla JS/CSS for scrubbed video, portal canvas, stacking cards, marquees, magnetic hover, preloader, cursor, horizontal scroll, and more.
- **Source prompts** for exact recreation of the three reference builds.

## Contents
- `SKILL.md` - metadata, activation description, and the 9-phase workflow (loaded when the skill triggers)
- `references/art-direction.md` - signature idea, archetypes, palette, type, composition, imagery
- `references/motion-and-scroll.md` - motion language, easing, scrollytelling, pinning, reduced motion, GSAP patterns
- `references/assets.md` - sourcing, licensing, optimization, image sequences, 3D, video/audio
- `references/tech-and-performance.md` - stack choice, Three.js practices, budgets, accessibility, responsive, cleanup
- `references/verification.md` - browser verification loop, viewport matrix, rubric, honest reporting
- `references/explainers-and-data.md` - visual explanation, interactive models, data narratives
- `references/style-selector.md` - how the best style is chosen automatically (topic table, scoring, combination rules)
- `references/style-library.md` - 26 styles S01-S26 + overlays O1-O4, each with fallbacks
- `references/taste-profile.md` - the quality bar and signature moves
- `references/technique-recipes.md` - R1-R20 working code recipes
- `references/source-prompts/` - three literal reference prompts (portfolio, portal, scroll-scrubbed film)

## Install
Agent skill formats differ; confirm your tool's current docs.
- **Claude.ai / Claude app:** open the `.skill` file card and click *Save skill*, or upload the folder/zip under Settings -> Capabilities -> Skills (menu names may vary).
- **Claude Code:** copy the `cinematic-experience-director/` folder to `~/.claude/skills/` (personal) or `<project>/.claude/skills/` (project), then restart the session.
- **Other agents (Cursor, Codex, etc.):** place `SKILL.md` and `references/` wherever that tool loads instructions/rules, or paste SKILL.md into its rules file and keep `references/` alongside. Compatibility with each tool is not verified here.

## Use
Just describe your goal: "Build a cinematic website for X", "Redesign this site: <path/url>", "Audit the motion on my landing page". Add references, assets, constraints, or a visual-intensity level (1-5) for better results. Say "plan only" to get the brief, art direction, and storyboard without code.

## Notes
- Optional companion skills (motion craft, design critique, taste guides) are used only if installed; the workflow works without them.
- The skill requires a browser tool (e.g., Playwright) for full visual verification; without one it will state that visuals are unverified.
