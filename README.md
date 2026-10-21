# Cinematic Experience Director

An AI skill that builds **distinctive, scrollytelling websites for any topic**. Give it a one-line prompt and it
invents a bespoke style for the subject, sources or generates high-quality assets, and builds a working,
motion-rich page, asking you questions only when something truly matters.

> "Create a scrollytelling website about black holes."  ->  a custom-styled, asset-rich page, no template.

## Features
- **Dynamic style synthesis:** finds a metaphor in your topic, picks the scroll/interaction mechanic that acts it
  out, then chooses palette, type, material and media. 26 seed styles act as vocabulary, never a fixed menu.
- **Asset pipeline:** searches, downloads, vets and grades stock video/photos, public-domain archives, 3D models,
  fonts, icons; designs logos/wordmarks; generates media when tools exist or builds procedural visuals.
  Every asset is documented in an `ASSETS.md` manifest with license and source.
- **Smart intake:** assumes everything it can infer. Vague prompt or "just build it" means zero questions. Otherwise
  it asks at most 4 relevant, high-impact questions (with defaults) before building.
- **Working code recipes (R1-R20):** scroll-scrubbed video, canvas portal windows, stacking cards, marquees,
  magnetic hover, preloaders, custom cursor, horizontal scroll, Three.js scroll camera, and more.
- **Browser-verified:** a mandatory verification loop and honest reporting of what was and was not tested.

## Repository layout
```
.
├── README.md
├── HOW-TO-USE.md                      # quick usage guide
├── START-HERE.md                      # instructions for any AI that receives this repo/zip
├── cinematic-experience-director.skill   # packaged skill (upload to Claude.ai)
└── cinematic-experience-director/
    ├── SKILL.md                       # workflow and rules (entry point)
    ├── README.md
    └── references/
        ├── intake-questions.md        # when to assume vs ask
        ├── style-synthesis.md         # inventing a bespoke style per project
        ├── style-library.md           # 26 seed styles + overlays
        ├── style-selector.md          # seed shortlisting by topic
        ├── taste-profile.md           # quality bar
        ├── taste-examples/            # 3 sample prompts, calibration only (not targets)
        ├── asset-pipeline.md          # sourcing, generating, vetting assets
        ├── assets.md                  # licensing and optimization
        ├── technique-recipes.md       # R1-R20 code recipes
        ├── art-direction.md, motion-and-scroll.md, tech-and-performance.md,
        │   verification.md, explainers-and-data.md
```

## Install
**Claude.ai / Claude app**
1. Settings -> Capabilities -> Skills (menu names may vary).
2. Upload `cinematic-experience-director.skill` (or a zip of the `cinematic-experience-director/` folder).

**Claude Code**
```bash
git clone <your-repo-url>
cp -r cinematic-experience-director ~/.claude/skills/            # personal
# or: cp -r cinematic-experience-director <project>/.claude/skills/   # per project
```
Restart the session afterwards.

**Other agents (Cursor, Codex, etc.)**
Place `SKILL.md` and `references/` where the tool loads instructions, or paste `SKILL.md` into its rules file and
keep `references/` alongside. Compatibility is not verified for every tool.

**No install (any chat):** attach the repo as a zip and say "follow START-HERE.md".

## Usage
Just describe the site:
```
Create a scrollytelling website about the history of Gujarat textiles.
Scrollytelling site for my specialty coffee roastery.
Portfolio for a 3D artist named Riya, dark and premium. Visual intensity 5/5.
Plan only: scrollytelling site about deep-sea internet cables.
```
Optional: upload your logo/photos/videos/brand colors, paste links or "I love X, hate Y" for taste, ask for a stack
("use React + Tailwind + Framer Motion"; default is one self-contained HTML file).

## How it works (pipeline)
1. **Intake:** infer vs ask (`intake-questions.md`).
2. **Style synthesis:** metaphor -> mechanic -> world -> Style Brief (`style-synthesis.md`).
3. **Storyboard:** scenes, not sections.
4. **Asset acquisition:** brief -> source/generate -> quality gate -> `ASSETS.md` (`asset-pipeline.md`).
5. **Build:** smallest coherent stack, recipes from `technique-recipes.md`.
6. **Verify:** real browser at multiple viewports, reduced-motion, asset-failure tests.

## Notes and limits
- Some environments restrict network access, so downloads can fail; the skill then falls back to verified links,
  procedural visuals, or placeholders, and tells you which assets to replace.
- The three files in `references/taste-examples/` recreate third-party sites and contain example asset URLs. They are
  taste calibration only. Remove that folder if you do not want third-party material in your public repo.
- Respect asset licenses and attribution; the skill records them but you are responsible for final compliance.

## License
Add a license of your choice (for example MIT) before publishing. No license is included by default.
