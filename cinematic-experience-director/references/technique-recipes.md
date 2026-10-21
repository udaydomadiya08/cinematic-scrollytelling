# Technique Recipes (R1-R21)

Dependency-free snippets (vanilla JS/CSS) for the techniques used by the styles in
`style-library.md`. Adapt names/values; keep the mechanics. All scroll code is passive, uses
`transform`/`opacity`, and respects reduced motion (R16). Test each in a real browser.

## Contents
R1 Scroll progress + lerp loop - R2 Scroll-scrubbed video (a seek, b frame cache) - R3 Letter-by-letter scroll text -
R4 Scroll-driven dual marquee - R5 Sticky stacking cards - R6 Magnetic element - R7 Reveal system -
R8 Canvas portal window (fake 3D) - R9 Preloader counter + docked logo - R10 Custom cursor -
R11 Horizontal scroll section - R12 Type-as-window / mask - R13 Image-sequence canvas - R14 Pinned chapters -
R15 Tokens: gradient type, glass, inversion seam - R16 Reduced motion - R17 SVG path draw - R18 Three.js scroll camera -
R19 Spotlight mask - R20 Velocity-skew marquee - R21 3D Diagonal Explode & Re-Merge Assembly Mechanism

## R1 Scroll progress + lerp loop
```js
const clamp = (v, a = 0, b = 1) => Math.min(b, Math.max(a, v));
const lerp = (a, b, t) => a + (b - a) * t;
// progress of a tall track element: 0 when its top hits viewport top, 1 when its bottom hits viewport bottom
function trackProgress(el) {
  const r = el.getBoundingClientRect();
  return clamp(-r.top / (r.height - innerHeight));
}
let smooth = 0;
function loop() {
  const target = trackProgress(document.querySelector('.track'));
  smooth = lerp(smooth, target, 0.12);          // 0.08 floaty - 0.2 tight
  document.documentElement.style.setProperty('--p', smooth.toFixed(4));
  requestAnimationFrame(loop);
}
requestAnimationFrame(loop);
```

## R2 Scroll-scrubbed video
**Encode for scrubbing** (all keyframes = smooth seeking): `ffmpeg -i in.mp4 -an -vf scale=1920:-2 -c:v libx264 -g 1 -crf 23 -pix_fmt yuv420p -movflags +faststart scrub.mp4`.
Structure: `.track{height:500vh}` > `.stage{position:sticky;top:0;height:100vh}` > video/canvas.

### R2a Seek approach (simple)
```js
const v = document.querySelector('video'); // muted playsinline preload="auto"; no autoplay
let cur = 0;
function tick() {
  const target = trackProgress(document.querySelector('.track'));
  cur = lerp(cur, target, 0.12);
  if (v.readyState >= 2 && v.duration) {
    const t = cur * (v.duration - 0.05);
    if (Math.abs(v.currentTime - t) > 0.04) v.currentTime = t;
  }
  requestAnimationFrame(tick);
}
tick();
```
### R2b Frame cache approach (smoothest)
```js
async function cacheFrames(url, max = 90, width = 960) {
  const v = document.createElement('video');
  v.src = url; v.muted = true; v.playsInline = true; v.crossOrigin = 'anonymous'; v.preload = 'auto';
  await new Promise((res, rej) => { v.onloadeddata = res; v.onerror = rej; });
  await new Promise(r => setTimeout(r, 300));
  const n = Math.max(24, Math.min(max, Math.round(v.duration * 12)));
  const h = Math.round(width * v.videoHeight / v.videoWidth);
  const frames = [];
  for (let i = 0; i < n; i++) {
    v.currentTime = (i / (n - 1)) * (v.duration - 0.05);
    await new Promise(r => v.onseeked = r);
    frames.push(await createImageBitmap(v, { resizeWidth: width, resizeHeight: h }));
  }
  return frames;
}
function drawCover(ctx, img, W, H) {       // object-fit: cover
  const s = Math.max(W / img.width, H / img.height);
  const w = img.width * s, h = img.height * s;
  ctx.drawImage(img, (W - w) / 2, (H - h) / 2, w, h);
}
// in loop: const i = Math.round(cur * (frames.length - 1)); drawCover(ctx, frames[i], W, H);
```
Cross-origin video needs CORS headers to draw to canvas; if blocked, fall back to R2a. Layer order:
poster `<img>` -> `<video>` -> `<canvas>`; fade each out (500ms) when the next is ready.
DPR: `Math.min(devicePixelRatio, 2)`.

## R3 Letter-by-letter scroll text
```js
function splitChars(el) {
  const text = el.textContent; el.textContent = '';
  return [...text].map(ch => {
    const s = document.createElement('span');
    s.textContent = ch; s.style.opacity = .2; s.style.transition = 'opacity .1s linear';
    el.appendChild(s); return s;
  });
}
const p = document.querySelector('.reveal-text'), chars = splitChars(p);
function update() {
  const r = p.getBoundingClientRect();
  // 0 when top hits 80% of viewport, 1 when bottom hits 20%
  const prog = clamp((innerHeight * 0.8 - r.top) / (innerHeight * 0.6 + r.height));
  const n = chars.length;
  chars.forEach((c, i) => c.style.opacity = (0.2 + 0.8 * clamp(prog * n - i)).toFixed(3));
}
addEventListener('scroll', update, { passive: true }); update();
```
Keep an `aria-label` with the full text on the paragraph and `aria-hidden` on spans.

## R4 Scroll-driven dual marquee
```html
<section class="marquee"><div class="row" data-dir="1"></div><div class="row" data-dir="-1"></div></section>
```
```js
const sec = document.querySelector('.marquee'), rows = [...sec.querySelectorAll('.row')];
function marquee() {
  const top = sec.getBoundingClientRect().top + scrollY;
  const offset = (scrollY - top + innerHeight) * 0.3;
  rows.forEach(r => r.style.transform = `translate3d(${(+r.dataset.dir) * (offset - 200)}px,0,0)`);
}
addEventListener('scroll', marquee, { passive: true }); marquee();
```
CSS: `.row{display:flex;gap:12px;width:max-content;will-change:transform}` tiles 420x270, `border-radius:1rem`,
`object-fit:cover`, `loading="lazy"`. Triple each row's tiles for length. Row 1 moves right, row 2 left.

## R5 Sticky stacking cards
```html
<div class="stack"> <div class="slot"><article class="card">...</article></div> ... </div>
```
```css
.slot{height:85vh}
.card{position:sticky;top:calc(6rem + var(--i)*28px);border-radius:60px;transform-origin:top center;will-change:transform}
```
```js
const slots = [...document.querySelectorAll('.slot')], N = slots.length;
slots.forEach((s, i) => s.firstElementChild.style.setProperty('--i', i));
function stack() {
  slots.forEach((s, i) => {
    const card = s.firstElementChild, target = 1 - (N - 1 - i) * 0.03;
    const r = s.getBoundingClientRect();
    // progress while the *next* slot pushes this card; 0 -> 1 over one slot height
    const prog = clamp(-r.top / s.offsetHeight);
    card.style.transform = `scale(${lerp(1, target, prog)})`;
  });
}
addEventListener('scroll', stack, { passive: true }); stack();
```

## R6 Magnetic element
```js
function magnet(el, { padding = 150, strength = 3 } = {}) {
  let on = false;
  addEventListener('pointermove', e => {
    const r = el.getBoundingClientRect(), cx = r.left + r.width / 2, cy = r.top + r.height / 2;
    const near = Math.abs(cx - e.clientX) < r.width / 2 + padding && Math.abs(cy - e.clientY) < r.height / 2 + padding;
    if (near) { el.style.transition = 'transform .3s ease-out'; el.style.transform = `translate3d(${(e.clientX - cx) / strength}px,${(e.clientY - cy) / strength}px,0)`; on = true; }
    else if (on) { el.style.transition = 'transform .6s ease-in-out'; el.style.transform = 'translate3d(0,0,0)'; on = false; }
  });
}
```
Skip on touch (`matchMedia('(pointer:fine)')`).

## R7 Reveal system (blur + rise + stagger)
```css
[data-reveal]{opacity:0;transform:translateY(32px);filter:blur(8px);
  transition:opacity .8s cubic-bezier(.22,1,.36,1),transform .8s cubic-bezier(.22,1,.36,1),filter .8s cubic-bezier(.22,1,.36,1);
  transition-delay:var(--d,0ms);will-change:transform,opacity}
[data-reveal].in{opacity:1;transform:none;filter:blur(0)}
```
```js
const io = new IntersectionObserver(es => es.forEach(e => { if (e.isIntersecting) { e.target.classList.add('in'); io.unobserve(e.target); } }), { threshold: .15 });
document.querySelectorAll('[data-reveal]').forEach(el => io.observe(el));
// usage: <h1 data-reveal style="--d:280ms">
```

## R8 Canvas portal window (fake 3D) - core of S02
```js
const cv = document.getElementById('portal-canvas'), ctx = cv.getContext('2d');
function resize() { const d = Math.min(devicePixelRatio || 1, 2); cv.width = innerWidth * d; cv.height = innerHeight * d;
  cv.style.width = innerWidth + 'px'; cv.style.height = innerHeight + 'px'; ctx.setTransform(d, 0, 0, d, 0, 0); }
addEventListener('resize', resize); resize();

function rrPoints(w, h, r) {            // ~44 points around a rounded rect, centred at origin
  r = Math.min(r, w / 2, h / 2); const pts = [];
  const arcs = [[w/2-r, -h/2+r, -Math.PI/2, 0], [w/2-r, h/2-r, 0, Math.PI/2], [-w/2+r, h/2-r, Math.PI/2, Math.PI], [-w/2+r, -h/2+r, Math.PI, Math.PI*1.5]];
  for (const [cx, cy, a0, a1] of arcs) for (let i = 0; i <= 10; i++) { const a = a0 + (a1 - a0) * i / 10; pts.push([cx + Math.cos(a) * r, cy + Math.sin(a) * r]); }
  return pts;
}
function project([x, y], rx, ry, cx, cy, f = 850) {   // rx, ry in degrees
  const ax = rx * Math.PI / 180, ay = ry * Math.PI / 180;
  const xx = x * Math.cos(ay), yy = y * Math.cos(ax), z = x * Math.sin(ay) - y * Math.sin(ax), p = f / (f + z);
  return [cx + xx * p, cy + yy * p];
}
let rotX = 0, rotY = 0, tX = 0, tY = 0, e = 0 /* expansion 0..1 */, maskScale = 1, last = performance.now();
addEventListener('pointermove', ev => { tY = (ev.clientX / innerWidth - .5) * 37.4; tX = (ev.clientY / innerHeight - .5) * -33; });
document.addEventListener('pointerleave', () => { tX = tY = 0; });
const ease = t => t < .5 ? 4*t*t*t : 1 - Math.pow(-2*t + 2, 3) / 2;
function animate(set, ms) { return new Promise(res => { const t0 = performance.now();
  (function f(n) { const t = Math.min(1, (n - t0) / ms); set(ease(t)); t < 1 ? requestAnimationFrame(f) : res(); })(t0); }); }

function drawCover(media) { const mw = media.videoWidth || media.naturalWidth || media.width, mh = media.videoHeight || media.naturalHeight || media.height;
  if (!mw) return; const s = Math.max(innerWidth / mw, innerHeight / mh), w = mw * s, h = mh * s; ctx.drawImage(media, (innerWidth - w) / 2, (innerHeight - h) / 2, w, h); }

function frame(now, getMedia, anchorEl) {
  const dt = Math.min(40, now - last); last = now;
  rotX += (tX - rotX) * Math.min(1, dt * .009); rotY += (tY - rotY) * Math.min(1, dt * .009);
  ctx.clearRect(0, 0, innerWidth, innerHeight);
  const r = anchorEl.getBoundingClientRect(), rcx = r.left + r.width / 2, rcy = r.top + r.height / 2;
  const cx = rcx + (innerWidth / 2 - rcx) * e, cy = rcy + (innerHeight / 2 - rcy) * e;
  const s = e ? 1 : maskScale, w = (r.width + (innerWidth - r.width) * e) * s, h = (r.height + (innerHeight - r.height) * e) * s;
  if (w > 1 && h > 1) {
    const pts = rrPoints(w, h, 90 * (1 - e) * s).map(p => project(p, rotX * (1 - e), rotY * (1 - e), cx, cy));
    ctx.save(); ctx.beginPath(); pts.forEach((p, i) => i ? ctx.lineTo(p[0], p[1]) : ctx.moveTo(p[0], p[1])); ctx.closePath(); ctx.clip();
    ctx.fillStyle = '#030303'; ctx.fillRect(0, 0, innerWidth, innerHeight); drawCover(getMedia()); ctx.restore();
  }
}
// travel: await animate(v => e = v, 1100); then play the transition film, freeze last frame, swap state, reopen: e = 0; await animate(v => maskScale = v, 1050)
```
The media is **screen-locked** (cover-drawn full-screen and clipped), so the window moves over a stationary picture.
Keep the real `<video>`/`<img>` elements hidden (1px, `visibility:hidden`) as pixel sources.
Procedural fallback: pass a second offscreen canvas as `getMedia()` that paints the state's generative scene.

## R9 Preloader counter + docked logo
```css
.logo{position:fixed;left:50%;top:50%;transform:translate(-50%,-50%);width:59px;transition:all 2s cubic-bezier(.16,1,.3,1);z-index:22}
.logo.docked{left:clamp(18px,1.95vw,28px);top:clamp(18px,3.1vh,28px);width:37px;transform:none}
.count{position:fixed;left:50%;bottom:28px;transform:translateX(-50%);font-weight:100;font-size:64px;z-index:22}
.count.leaving{animation:out .75s cubic-bezier(.22,1,.36,1) both}
@keyframes out{to{opacity:0;filter:blur(7px);transform:translate(-50%,-34px)}}
```
```js
async function preload(urls, onProgress) { let done = 0;
  await Promise.all(urls.map(u => fetch(u).then(r => r.blob()).catch(() => 0).then(() => onProgress(++done / urls.length)))); }
// show Math.round(progress*100) eased toward real progress; at 100: .leaving on counter, .docked on logo, then start the experience
```
Tie the number to real work (assets or a short intro film's `currentTime/duration`), never a fake timer longer than ~3s.

## R10 Custom cursor (dot + lerped ring + label)
```js
if (matchMedia('(pointer:fine)').matches) {
  const ring = document.querySelector('.ring'), dot = document.querySelector('.dot');
  let x = 0, y = 0, rx = 0, ry = 0;
  addEventListener('pointermove', e => { x = e.clientX; y = e.clientY; dot.style.transform = `translate3d(${x}px,${y}px,0) translate(-50%,-50%)`; });
  (function f() { rx += (x - rx) * .2; ry += (y - ry) * .2; ring.style.transform = `translate3d(${rx}px,${ry}px,0) translate(-50%,-50%)`; requestAnimationFrame(f); })();
  document.querySelectorAll('[data-cursor]').forEach(el => {
    el.addEventListener('pointerenter', () => { ring.classList.add('active'); ring.dataset.label = el.dataset.cursor; });
    el.addEventListener('pointerleave', () => ring.classList.remove('active'));
  });
  document.documentElement.classList.add('no-cursor');   // html.no-cursor,html.no-cursor *{cursor:none}
}
```
Dot 12px white; ring 36px with 1px border + 40% white fill; label fades in below on `.active` (ring scales ~1.16).

## R11 Horizontal scroll section
```css
.hs{height:var(--h)} .hs-stage{position:sticky;top:0;height:100vh;overflow:hidden} .hs-track{display:flex;gap:2vw;height:100%;align-items:center;will-change:transform}
```
```js
const hs = document.querySelector('.hs'), trk = hs.querySelector('.hs-track');
function setH() { hs.style.setProperty('--h', trk.scrollWidth - innerWidth + innerHeight + 'px'); }
function hscroll() { const p = clamp(-hs.getBoundingClientRect().top / (hs.offsetHeight - innerHeight)); trk.style.transform = `translate3d(${-p * (trk.scrollWidth - innerWidth)}px,0,0)`; }
addEventListener('resize', setH); addEventListener('scroll', hscroll, { passive: true }); setH(); hscroll();
```
On touch, prefer native `overflow-x:auto; scroll-snap-type:x mandatory` instead.

## R12 Type-as-window / mask
```css
.window-type{font:900 28vw/0.8 'Anton',Impact,sans-serif;text-transform:uppercase;
  background:url(poster.jpg) center/cover;-webkit-background-clip:text;background-clip:text;color:transparent}
```
For video inside glyphs use an SVG mask:
```html
<svg width="100%" height="100%"><defs><mask id="m"><rect width="100%" height="100%" fill="#000"/><text x="50%" y="62%" text-anchor="middle" fill="#fff" font-size="30vw" font-weight="900">ON</text></mask></defs>
<foreignObject width="100%" height="100%" mask="url(#m)"><video src="film.mp4" muted loop playsinline autoplay style="width:100%;height:100%;object-fit:cover"></video></foreignObject></svg>
```
"Fall through the O": scale the masked layer `scale(1 + p*40)` around the counter-shape centre while cross-fading the next scene.

## R13 Image-sequence canvas
```js
const N = 120, imgs = [], cv = document.querySelector('canvas'), ctx = cv.getContext('2d');
for (let i = 1; i <= N; i++) { const im = new Image(); im.src = `frames/${String(i).padStart(4, '0')}.webp`; imgs.push(im); }
function seq() { const p = trackProgress(document.querySelector('.track')); const im = imgs[Math.round(p * (N - 1))];
  if (im.complete) { cv.width = cv.width; drawCover(ctx, im, cv.width, cv.height); } requestAnimationFrame(seq); }
```
Load the first ~10 frames eagerly, the rest progressively; show frame 1 as poster. (Reuse `drawCover` from R2b.)

## R14 Pinned chapters (sticky stage + steps)
```html
<section class="chapters"><div class="stage" data-step="0">...visual...</div>
 <div class="steps"><article data-i="0"></article><article data-i="1"></article>...</div></section>
```
```css
.chapters{display:grid;grid-template-columns:1fr 1fr}.stage{position:sticky;top:0;height:100vh}.steps article{min-height:100vh}
```
```js
const stage = document.querySelector('.stage');
const io2 = new IntersectionObserver(es => es.forEach(e => { if (e.isIntersecting) stage.dataset.step = e.target.dataset.i; }), { rootMargin: '-50% 0px -50% 0px' });
document.querySelectorAll('.steps article').forEach(a => io2.observe(a));
```
Drive visuals with `.stage[data-step="2"] .part-b{...}` CSS so scrolling back reverses automatically.

## R15 Tokens: gradient type, glass, inversion seam
```css
:root{--ground:#0C0C0C;--ink:#D7E2EA}
.hero-heading{background:linear-gradient(180deg,#646973 0%,#BBCCD7 100%);-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;font-weight:900;text-transform:uppercase;letter-spacing:-.02em;line-height:.9;font-size:clamp(3rem,17.5vw,260px)}
.pill-cta{border-radius:999px;color:#fff;text-transform:uppercase;letter-spacing:.14em;padding:14px 44px;
  background:linear-gradient(123deg,#18011F 7%,#B600A8 37%,#7621B0 72%,#BE4C00 100%);box-shadow:0 4px 4px rgba(181,1,167,.25),4px 4px 12px #7721B1 inset;outline:2px solid #fff;outline-offset:-3px}
.glass{background:rgba(255,255,255,.12);-webkit-backdrop-filter:blur(12px);backdrop-filter:blur(12px);border:1px solid rgba(255,255,255,.18)}
.badge{border-left:2px solid #fff;background:rgba(255,255,255,.15);backdrop-filter:blur(12px);padding:6px 12px;font:11px ui-monospace,monospace;text-transform:uppercase;letter-spacing:.15em}
.on-media{color:#fff;text-shadow:0 2px 12px rgba(0,0,0,.45)}
.seam{background:#fff;color:var(--ground);border-radius:60px 60px 0 0;margin-top:-56px;position:relative;z-index:5}
```
Swap the accent gradient for one derived from the subject; keep one accent per page.

## R16 Reduced motion + fallbacks
```css
@media (prefers-reduced-motion:reduce){*,*::before,*::after{animation-duration:.01ms!important;animation-iteration-count:1!important;transition-duration:.01ms!important;scroll-behavior:auto!important}
  [data-reveal]{opacity:1;transform:none;filter:none}}
```
```js
const reduce = matchMedia('(prefers-reduced-motion:reduce)').matches;  // skip scrub/parallax/marquee; show poster; show final text state
```

## R17 SVG path draw / point-on-path
```js
const path = document.querySelector('#route'), L = path.getTotalLength();
path.style.strokeDasharray = L; path.style.strokeDashoffset = L;
function draw() { const p = trackProgress(document.querySelector('.track')); path.style.strokeDashoffset = L * (1 - p);
  const pt = path.getPointAtLength(L * p); marker.setAttribute('transform', `translate(${pt.x},${pt.y})`); }
addEventListener('scroll', draw, { passive: true });
```

## R18 Three.js scroll camera (minimal)
Load a pinned build from an allowed CDN (e.g. cdnjs `three.js/r128/three.min.js`, global `THREE`; for newer
releases use an ES module from jsDelivr with an exact version).
```js
const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
renderer.setPixelRatio(Math.min(devicePixelRatio, 1.75));
const scene = new THREE.Scene(), cam = new THREE.PerspectiveCamera(40, innerWidth / innerHeight, .1, 100);
const mesh = new THREE.Mesh(new THREE.TorusKnotGeometry(1, .32, 220, 24), new THREE.MeshStandardMaterial({ color: 0xdfe6ee, roughness: .25, metalness: .85 }));
scene.add(mesh, new THREE.HemisphereLight(0xffffff, 0x222233, 1.2), Object.assign(new THREE.DirectionalLight(0xffffff, 2), { position: new THREE.Vector3(3, 4, 5) }));
let p = 0;
(function f() { p = lerp(p, trackProgress(document.querySelector('.track')), .08);
  cam.position.set(Math.sin(p * Math.PI) * 5, 1 + p * 2, 6 - p * 3); cam.lookAt(0, 0, 0); mesh.rotation.y = p * Math.PI * 2;
  renderer.render(scene, cam); requestAnimationFrame(f); })();
addEventListener('resize', () => { renderer.setSize(innerWidth, innerHeight); cam.aspect = innerWidth / innerHeight; cam.updateProjectionMatrix(); });
```
Pause rendering when off-screen (IntersectionObserver); dispose geometries/materials on teardown; provide a poster if WebGL fails.

## R19 Spotlight mask
```css
.hidden-layer{position:absolute;inset:0;-webkit-mask:radial-gradient(circle 140px at var(--x,50%) var(--y,50%),#000 0,#000 60%,transparent 100%);mask:radial-gradient(circle 140px at var(--x,50%) var(--y,50%),#000 0,#000 60%,transparent 100%)}
```
```js
addEventListener('pointermove', e => { const s = document.documentElement.style; s.setProperty('--x', e.clientX + 'px'); s.setProperty('--y', e.clientY + 'px'); });
```

## R20 Velocity-skew marquee (S11)
```js
let lastY = scrollY, vel = 0, x = 0;
(function f() { vel = lerp(vel, scrollY - lastY, .1); lastY = scrollY; x -= 1.2 + Math.abs(vel) * .5;
  const row = document.querySelector('.kinetic'); const w = row.scrollWidth / 2; row.style.transform = `translate3d(${x % w}px,0,0) skewX(${clamp(vel * -.4, -12, 12)}deg)`; requestAnimationFrame(f); })();
```
Duplicate the row content once so `x % w` loops seamlessly.

## R21 3D Diagonal Explode & Re-Merge Assembly Mechanism (S27)
Used for hardware startups, audio/earphone showcases, watch movements, robotics, and consumer electronics where components separate along an engineered 38.4° 3D diagonal vector, orbit 360°, and magnetically re-merge back together upon scroll.

### 1. 5-Stage Timeline State Evaluator
```js
function evaluateExplodeTimeline(p) {
  p = Math.min(1, Math.max(0, p));
  // 0.00-0.14: Assembled | 0.14-0.42: Explodes | 0.42-0.65: Full Breakdown | 0.65-0.87: Re-Merges | 0.87-1.00: Locked
  let explosion = 0;
  if (p < 0.14) explosion = 0;
  else if (p < 0.42) explosion = (p - 0.14) / 0.28;
  else if (p < 0.65) explosion = 1.0;
  else if (p < 0.87) explosion = 1.0 - (p - 0.65) / 0.22;
  else explosion = 0;

  const diagRoll = -38.4 * Math.PI / 180; // 38.4 deg diagonal 3D vector
  const yaw = -0.45 + p * Math.PI * 2.15;
  const pitch = 0.24 + Math.sin(p * Math.PI * 2) * 0.22;
  const lockPulse = (p >= 0.85 && p <= 0.98) ? Math.sin(((p - 0.85) / 0.13) * Math.PI) : 0;
  return { p, explosion, diagRoll, yaw, pitch, lockPulse };
}
```

### 2. 3D-to-2D Perspective Projection along Diagonal Vector
```js
function project3D(lx, ly, lz, state, cx, cy, scalePx) {
  // Yaw -> Pitch -> Diagonal 38.4 deg Roll
  const cyaw = Math.cos(state.yaw), syaw = Math.sin(state.yaw);
  let x1 = lx * cyaw + lz * syaw, y1 = ly, z1 = -lx * syaw + lz * cyaw;
  const cpitch = Math.cos(state.pitch), spitch = Math.sin(state.pitch);
  let x2 = x1, y2 = y1 * cpitch - z1 * spitch, z2 = y1 * spitch + z1 * cpitch;
  const croll = Math.cos(state.diagRoll), sroll = Math.sin(state.diagRoll);
  let x3 = x2 * croll - y2 * sroll, y3 = x2 * sroll + y2 * croll;
  const persp = 9.5 / (9.5 + z2 + 4.2);
  return { x: cx + x3 * scalePx * persp, y: cy + y3 * scalePx * persp, z: z2, s: persp };
}
```

### 3. Component Interpolation (Assembled -> Exploded -> Re-Merged)
```js
// parts have resting offset along the axis (e.g., [-3.25, -2.15, -1.10, 0, 1.18, 2.28, 3.35])
parts.forEach((part, idx) => {
  const assembledX = (idx - 3) * 0.22;
  const explodedX = part.offset;
  const curX = lerp(assembledX, explodedX, state.explosion);
  const pos = project3D(curX, 0, 0, state, cx, cy, scalePx);
  // draw procedural 3D cylinder or position Three.js sub-assembly at curX
});
```

