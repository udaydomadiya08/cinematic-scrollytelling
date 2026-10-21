# How to use the Cinematic Experience Director skill (v3: dynamic style + assets + smart questions)

## In a new chat
1. Attach this zip.
2. Write your request, even one line:
   - "Create a scrollytelling website about black holes."
   - "Scrollytelling site for my specialty coffee roastery."
   - "Portfolio for a 3D artist named Riya, dark and premium."
3. If your prompt is short or vague, Claude chooses everything automatically (style, palette, fonts, layout, motion, assets) and builds.
4. If something truly matters and cannot be guessed (your real brand name, logo/photos, a genuine taste choice), Claude asks a few sharp questions first (max 4, with defaults). Say "just build it" to skip all questions.

## What it does for you
- **Invents a style per topic** (not from a fixed list): finds a metaphor in your subject, a scroll mechanic that acts it out, and a matching world of colors, type and media.
- **Gets the best assets**: searches and verifies stock video/photos, public-domain archives, 3D models, fonts, icons; designs logos/wordmarks; generates media when tools exist, or builds procedural visuals; documents everything in `ASSETS.md`.
- **Verifies** the result in a browser when one is available and reports honestly.

## Optional controls
- Intensity: "visual intensity 5/5" (default 4).
- Give taste: paste links/screenshots/"I love X, hate Y" and it will extract the qualities.
- Provide assets: upload logo, photos, videos, brand colors; they take priority.
- Change direction: "switch to the second alternate" or "make it more calm/loud".
- Planning only: "plan only" returns the style brief, asset plan and storyboard.
- Stack: "use React + Tailwind + Framer Motion" (default: one self-contained HTML file).

## Files
| File | Purpose |
|---|---|
| SKILL.md | Workflow and rules |
| references/intake-questions.md | When to assume vs ask |
| references/style-synthesis.md | Inventing a bespoke style |
| references/style-library.md, style-selector.md | Seed styles and shortlist helper |
| references/taste-profile.md, taste-examples/ | Quality bar; your 3 samples as calibration only |
| references/asset-pipeline.md, assets.md | Sourcing, generating, vetting assets |
| references/technique-recipes.md | R1-R20 working code |
| other references | Art direction, motion, tech/performance, verification, explainers |

## Install permanently
Use the `.skill` file (Claude.ai: Settings -> Capabilities -> Skills) or copy the folder to `~/.claude/skills/` for Claude Code.
