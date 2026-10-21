# Asset Pipeline (assets are half of the quality)

A scrollytelling site is judged by its imagery, film, type, and details. Weak assets make
great code look cheap. This file is the mandatory process for **acquiring, generating, checking, and
documenting the best possible assets for each specific project**. It extends `assets.md`
(licensing, optimization, sequences, 3D) with the active sourcing workflow.

## Contents
1. Principles
2. Step 1 - Asset brief (derived from the project, never generic)
3. Step 2 - Capability check (what can I actually do here?)
4. Step 3 - Source by asset type (priority order)
5. Step 4 - Generate when sourcing falls short
6. Step 5 - Quality gate
7. Step 6 - Process and optimize
8. Step 7 - Manifest, attribution, honesty
9. Search query recipes
10. Fonts, icons, logos (details)
11. Asset needs by style family

## 1. Principles
- **Assets are first-class.** Acquire assets *before* committing to a rendering approach and before
  detailed layout; design around what exists. Real, relevant, high-resolution media beats stylized
  stand-ins; stand-ins beat low-quality or irrelevant media.
- **Everything is chosen from the topic and what the user said.** The user's own assets, brand colors,
  logos, photos, and wording come first; the rest is inferred from the subject, audience, and chosen style.
- **Highest quality available, then graded to one look.** Pick the best source resolution, then apply one
  consistent grade (color, contrast, grain) so mixed sources feel like one film.
- **Verified or not used.** Never invent a URL, never claim an asset was downloaded or checked when it
  was not, and never use an image just because a search returned it.
- **Respect rights.** Use public-domain/CC0/permissive-license sources or user-provided files. No scraped
  watermarked previews, no copyrighted characters, no real people's likeness without a license.

## 2. Step 1 - Asset brief
Derive from the storyboard (`SKILL.md` Phase 4) a table of **slots**. Example columns:

| Slot | Role in scene | Type | Spec | Mood / grade | Route | Fallback |
|---|---|---|---|---|---|---|
| hero-film | Scene 1 background, scrubbed | video | 1080p+, 8-20 s, slow camera, no text/watermark | cold, high contrast | stock video / generated | procedural canvas |
| product-still | Scene 4 | image | >=2400 px, transparent or clean ground | soft studio | user / stock / render | SVG object |
| icon-set | feature list | icons | single family, 1.5 px stroke | neutral | Lucide/Phosphor | inline SVG |
| display-font | all headlines | font | heavy, character fits mood | - | Google/Fontshare | system stack |

Include: hero media, section imagery, textures/grain, icons, logos/wordmark, fonts, 3D models/HDRI,
audio (optional, muted by default), map/data, favicon/OG image, poster frames.
Slots are specific (what is in the frame, camera, light, palette), derived from the subject - not
"nice background".

## 3. Step 2 - Capability check
Inspect which tools exist in this environment and say what you will use:
- **Web search / fetch** (find sources, verify pages, read licenses).
- **Image search tool** (find candidate images; still verify license on the source page).
- **Shell with network** (download, `ffprobe`, `ffmpeg`, image tools). Network may be allow-listed; if a
  host is blocked say so and try another route.
- **Image/video generation tools** (MCP connectors, generation APIs, design tools). Use them if present.
- **User uploads** (zip/images/videos). Inspect first.
- **Browser** (to view candidates and rendered result).
If downloading is impossible: reference stable CDN URLs only when verified reachable, always add a
poster/gradient fallback, and tell the user which assets should be replaced with local files.

## 4. Step 3 - Source by asset type (try in this order)
**Photographs**
1. User-supplied or the organization's official press/brand kit (best for real businesses/people/places).
2. Open-license libraries: Unsplash, Pexels, Pixabay (check each license page), Wikimedia Commons
   (read per-file license/attribution), Flickr Commons.
3. Public institutions (usually public domain/open access): NASA, ESA, NOAA, USGS, Smithsonian Open Access,
   The Met Open Access, Rijksmuseum, Library of Congress, Europeana, national archives.
**Video clips**
1. User-supplied footage.
2. Free stock video: Pexels Videos, Pixabay Videos, Coverr, Mixkit, Videvo (check clip license), Wikimedia
   Commons video, Internet Archive public-domain films, NASA/ESA media libraries.
3. Generated film (see section 5). Prefer 1080p+ landscape for scrubbing/backgrounds and 9:16 variants for mobile.
**3D / textures / HDRI**: Poly Haven (CC0 HDRIs, textures, models), ambientCG (CC0), Poly Pizza, Khronos glTF
sample assets, Sketchfab models filtered to CC-BY/CC0 (keep attribution), NASA/Smithsonian 3D.
**Illustrations / vector art**: unDraw-style sets only if they fit the concept; otherwise draw custom SVG.
**Icons**: pick ONE family per project - Lucide, Phosphor, Tabler, Iconoir, Heroicons. Match stroke weight to
the type weight. Avoid emoji as icons.
**Logos**: use the real logo only from the official source and only when the user supplied/approved it. For brand
marks of other companies, Simple Icons (SVG) can be used for neutral "works with" lists; respect trademarks. For a
new/fictional brand, **design a wordmark in SVG** (custom lettering or font + one distinctive detail) and a
favicon.
**Fonts**: Google Fonts, Fontshare, Bunny Fonts (privacy-friendly mirror), Fontsource, Open Foundry. See section 10.
**Audio** (optional, off by default): Freesound (check CC license), Pixabay audio, Mixkit.
**Maps and data**: Natural Earth, OpenStreetMap (attribution), national statistics, Our World in Data, NASA/NOAA
datasets. Cite sources in the page footer.
**Textures/grain/noise**: generate with SVG `feTurbulence`, CSS gradients, or canvas.

## 5. Step 4 - Generate when sourcing falls short
Use generation when the subject is fictional/abstract, when stock lacks the exact shot, or to keep a unified look.
- **AI image/video generation** (when a tool exists): write a *shot prompt* with: subject, action/camera move,
  lens/framing, lighting, color palette, materials, mood reference words, aspect ratio, duration, and negatives
  (no text, no watermark, no distorted hands/faces, no logos). Keep **one style bible** (palette, lighting,
  lens) reused across every prompt so assets match. Generate stills first, then animate/extend; loop-safe
  start/end frames for backgrounds. Inspect at full size and reject artifacts.
- **Procedural / code-generated**: canvas/WebGL generative film (flow field, noise sphere, nebula, particles),
  Three.js primitive models with PBR materials, SVG illustrations, CSS gradients, generative patterns. Treat as
  first-class when time/network is limited; label as stand-in when it replaces a photographic need.
- **Compositing**: grade + grain + vignette via CSS/canvas to unify mixed sources.
Always disclose AI-generated or procedural media in the report.

## 6. Step 5 - Quality gate (every asset passes before use)
| Check | Pass condition | How |
|---|---|---|
| Reachable & correct type | HTTP 200, expected content-type | `curl -sI`, `file` |
| Resolution | Hero image >= 2400 px wide; section image >= 1600; video >= 1080p; textures >= 2k | `identify`, `ffprobe` |
| Content | Matches the slot brief, no text/watermark/logo overlays, no obvious AI artifacts | view stills/frames |
| Composition | Leaves space for type; focal point where the layout expects | view in layout |
| Consistency | Lighting/color temperature compatible with siblings | grade or swap |
| Rights | License permits web use; attribution captured | record in manifest |
| Weight | Within budget (see section 7) | file size |
| Fallback | Poster/gradient exists | test with asset blocked |
Reject and re-source rather than shipping a mediocre asset. Aim for the best 80 %, not the first 100 %.

## 7. Step 6 - Process and optimize
```bash
# web video (muted background, fast start)
ffmpeg -i in.mp4 -an -vf "scale=-2:1080" -c:v libx264 -crf 23 -preset slow -pix_fmt yuv420p -movflags +faststart bg.mp4
# scrub-friendly (all keyframes)
ffmpeg -i in.mp4 -an -vf "scale=1920:-2" -c:v libx264 -g 1 -crf 24 -pix_fmt yuv420p -movflags +faststart scrub.mp4
# poster frame
ffmpeg -i bg.mp4 -frames:v 1 -q:v 2 poster.jpg
# frame sequence for canvas scrubbing
ffmpeg -i in.mp4 -vf "fps=24,scale=1280:-2" -c:v libwebp -quality 80 frames/%04d.webp
# images
python3 -c "from PIL import Image; im=Image.open('a.jpg'); im.thumbnail((2400,2400)); im.save('a.webp', quality=82)"
```
Budgets: hero video <= 8-15 MB; images 150-400 KB each; first-load total <= ~2-3 MB before the hero, lazy-load the
rest. Provide 9:16 or smaller variants for phones where it matters. Embed small assets (SVG, tiny posters) inline.

## 8. Step 7 - Manifest, attribution, honesty
Create `ASSETS.md` (or a comment block) listing for every asset: file/slot, source name + URL, author, license,
attribution required (yes/no, text), modifications, and whether it is real, stock, AI-generated, or procedural. Put
required attributions in the site footer or credits. In the final report, state which assets were verified and which
are stand-ins to replace.

## 9. Search query recipes
Build queries from the subject, the shot you need, and the mood; add quality words and source names.
- Video: `<subject> cinematic slow motion 4k stock footage pexels`, `<subject> aerial drone 4k`, `<subject> macro close up`,
  `<subject> timelapse`, `<subject> abstract background loop`.
- Photo: `<subject> editorial photography high resolution unsplash`, `<subject> texture macro`, `<subject> wikimedia commons`.
- Public domain science/space/history: `<subject> NASA image library`, `<subject> Smithsonian open access`, `<subject> Library of Congress`.
- 3D: `<subject> glb free CC0 poly pizza`, `polyhaven <material> texture`.
- Fonts: `<mood> display font fontshare`, `google fonts <mood> condensed display`.
Run several queries per slot, open candidates, compare 3-5, and choose the best; do not accept the first result.

## 10. Fonts, icons, logos (details)
- **Fonts - choose by mood, not habit.** Decide display voice first (monumental condensed, humanist serif, geometric
  grotesk, mono-technical, rounded friendly, high-contrast didone, hand-cut), then a quiet text face. Two families
  max plus optional mono. Check weights/axes available, set `font-display: swap`, preload the display font, and
  declare a metric-matched fallback. Variable fonts reduce files.
- **Icons**: one family, consistent stroke; inline SVG (no icon fonts); `aria-hidden` unless meaningful.
- **Logos/wordmarks**: simple, legible at 24 px, works on dark and light; supply SVG with `currentColor`. Never use a
  real company's logo as if the user were that company.
- **Favicon/OG**: generate an SVG favicon and an OG image from the hero still.

## 11. Asset needs by style family (quick lookup)
| Style family | Key assets | If unobtainable |
|---|---|---|
| Film-scrubbed / cinematic | 1-3 slow 1080p+ clips or generated film | procedural canvas film |
| Portal / destination | per-state background film/still + transition clip | per-state generative scene |
| Product sequence / 3D | 60-180 frames or GLB + HDRI | Three.js primitive model |
| Portfolio / agency | work thumbnails, cutout portrait/objects | generated cover cards |
| Editorial / documentary | real photography, captions | typographic cover + SVG |
| Data / explainer | real dataset, labeled | clearly-labeled illustrative data |
| Typographic / brutalist | fonts, sticker SVGs | native |
| Map / route | verified geography | abstract map |
Styles are invented per project (`style-synthesis.md`); derive needs from the storyboard, not from this table alone.
