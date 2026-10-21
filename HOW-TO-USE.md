# How to use the Cinematic Experience Director skill (v2: auto-style)

## In a new chat
1. Attach this zip.
2. Write one line, for example:
   - "Create a scrollytelling website about black holes."
   - "Scrollytelling site for my specialty coffee roastery in Ahmedabad."
   - "Portfolio for a 3D artist named Riya, dark and premium."
3. Claude reads the skill, picks the best-fit style from 26 styles, shows a short **Style Decision Record**, and builds a working page.

## Optional controls
- Intensity: "visual intensity 5/5" (default 4).
- Force a style: "use S02 portal style" or "make it like the planet portal" (see `references/style-library.md`).
- Switch after the first build: "switch to S05".
- Planning only: "plan only" returns style decision, brief, art direction and storyboard.
- Exact recreation: "recreate the Planet Jumping prompt exactly" uses `references/source-prompts/`.
- Stack: "use React + Tailwind + Framer Motion" (default is one self-contained HTML file).

## What is inside
| File | Purpose |
|---|---|
| SKILL.md | Workflow, style engine, quality criteria |
| references/style-selector.md | How the style is chosen (topic table, scoring) |
| references/style-library.md | S01-S26 styles + overlays |
| references/taste-profile.md | Your taste, distilled as a quality bar |
| references/technique-recipes.md | R1-R20 working code |
| references/source-prompts/ | Your three reference builds, verbatim |
| references/art-direction.md, motion-and-scroll.md, assets.md, tech-and-performance.md, verification.md, explainers-and-data.md | Original craft references |

## Notes
- The sample asset URLs from the reference prompts may expire or be blocked; the skill uses procedural fallbacks and never claims assets it did not verify.
- To install permanently: use the `.skill` file (Claude.ai: Settings -> Capabilities -> Skills) or copy the folder to `~/.claude/skills/` for Claude Code.
