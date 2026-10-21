# Asset Reference

## Contents
1. Asset audit
2. Sourcing and verification
3. Licensing
4. Optimization targets
5. Image sequences
6. 3D models and textures
7. Video and audio
8. Fallbacks and honesty

## 1. Asset audit
Before choosing a technique, list: photography, video, image sequences, 3D models, terrain/geo data, textures/HDRIs, illustrations/diagrams, icons, fonts, audio, datasets. For each: required? source? format? size budget? license? fallback?

## 2. Sourcing and verification
- Prefer: user-supplied assets, official brand/press kits, public-domain/CC0 libraries, properly licensed stock, self-made procedural/vector assets, generated assets (labeled as such, inspected at full resolution).
- Verify by actually downloading/fetching and opening the file: confirm it exists, decodes, dimensions, size, and visual quality.
- Search results, memory, or a plausible-looking URL are NOT evidence. Never invent URLs. Never write "downloaded X" unless a file is present on disk.
- Keep a manifest (`ASSETS.md` or `assets.json`): file, source URL, license, author, attribution text, modifications, date verified.
- If network access is restricted, say so and ask the user to supply files, or use verified procedural/vector alternatives.

## 3. Licensing
- Check the license of the specific item, not the site. Note: CC0 = no attribution needed; CC-BY = attribution required; CC-BY-NC = no commercial use; "free to use" is not a license.
- Government/agency media (e.g., NASA, Smithsonian open access) is often reusable but check each item's usage guidelines (logos, people, third-party content excluded).
- Marketplaces such as Sketchfab have per-model licenses; Poly Haven assets are CC0.
- Fonts and icon sets have licenses too. Record them.
- Never use trademarked logos or copyrighted characters/footage without the user's confirmation of rights.

## 4. Optimization targets
- Images: AVIF/WebP with JPEG/PNG fallback where needed; `srcset`/`sizes`; explicit `width`/`height`; `loading="lazy"` below the fold; `fetchpriority="high"` on the LCP image; no image larger than needed (typically <= 2x displayed size).
- Budget guideline: initial route critical path ideally under ~1-1.5 MB transferred on mobile; heavy cinematic content streams in after first paint with a designed loading state.
- SVG: run through SVGO, outline text if font not loaded, avoid giant path counts.
- Fonts: subset; WOFF2 only; limit weights.

## 5. Image sequences (scrubbed frames)
- Use when a high-fidelity pre-rendered move must scrub with scroll.
- Typical: 60-180 frames, 1280-1920 px wide on desktop, smaller set for mobile, WebP/AVIF each ~30-120 KB.
- Draw to `<canvas>`; preload progressively (first frame immediately, then in chunks); show a poster until ready; cap decode work per frame; handle high-DPI with a sensible max scale.
- Provide a static fallback frame for reduced motion and load failure.
- Alternative: short `<video>` with `currentTime` scrubbing works only with keyframe-dense encodes (all-intra or short GOP) - test it; otherwise frames are more reliable.

## 6. 3D models and textures
- Format: glTF/GLB. Compress with Draco or meshopt; textures as KTX2/Basis where supported.
- Budget guideline: hero model ideally under ~2-5 MB, <100k triangles for mobile-targeted scenes; fewer draw calls; reuse materials; bake lighting/AO where possible.
- HDRI: 1k-2k for lighting; use blurred/low-res for background if not showcased.
- Confirm the model's scale, pivot, and orientation; normalize on load. Check for missing textures and flipped normals.
- Dispose geometries, materials, textures, and render targets on unmount.

## 7. Video and audio
- Video: H.264 MP4 baseline + WebM/AV1 optional; `muted playsinline` for autoplay; poster frame; no autoplay with sound; keep loops short.
- Provide captions/transcripts for meaningful speech.
- Audio is opt-in: never autoplay; remember the user's choice; visible mute control.

## 8. Fallbacks and honesty
- Every heavy asset has a defined failure state (poster, static image, simplified layout).
- If a preferred asset was unavailable, use a verified alternative and state the compromise in the final report.
- Credits/attribution live somewhere discoverable (footer or credits page) and in the manifest.

## 9. Reference-prompt assets and AI-generated media
- The files in `source-prompts/` contain example CloudFront/CDN URLs for videos, 3D renders, and icons. They may expire or be blocked in a given environment. Verify with a real request before relying on them; otherwise use procedural stand-ins.
- Styles S02/S03/S05 are best with short AI-generated or rendered films. If none exist, build a procedural canvas/WebGL "film" (flow field, nebula, noise sphere, orbiting shapes) whose time parameter is driven by the same progress value; say plainly that it is a stand-in.
- Videos for scrubbing should be re-encoded all-keyframe (see `technique-recipes.md` R2) and kept under ~15 MB; provide a poster frame.
