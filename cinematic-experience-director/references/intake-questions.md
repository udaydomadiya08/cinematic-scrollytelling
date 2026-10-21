# Intake: When to Assume, When to Ask

Principle: **assume everything that can be inferred; ask only what would materially change the
result or what only the user can know.** Questions are generated *per project* from its real unknowns -
never a fixed questionnaire, never filler.

## Contents
1. Decision rule
2. Always assume (never ask)
3. Worth asking (when genuinely unknown)
4. Procedure
5. How to ask (format)
6. Question patterns (examples, not a script)
7. Reading taste from what the user gives you
8. After the answers

## 1. Decision rule
For each unknown, estimate **Impact** (how much the result changes) x **Cost of a wrong guess** (how
annoying/expensive to redo) x **Inferability** (can the topic/context answer it?).
- High impact AND high cost AND not inferable -> **ask**.
- Otherwise -> **assume**, state the assumption, and keep going.
If the user's message is short/vague, says "just build it", "surprise me", "you decide", or gives only a topic,
**do not ask**: choose everything, show the assumptions, build. They can redirect afterward.

## 2. Always assume (never ask)
Visual style and style mix, palette, fonts, layout, section order, motion language, scroll mechanics,
stack/file format, asset sourcing route, copy tone when the subject suggests it, section count, animation
intensity (default 4/5), responsive details. These are the skill's job.

## 3. Worth asking (only when truly unknown and it matters)
- **Real-world facts only the user has:** brand/person/business name, location, offerings/prices, links, contact,
  legal text, team names, real statistics, testimonials.
- **Must-use assets:** do they have a logo, photos, videos, brand colors/fonts? (Ask once, offer "source them for me".)
- **Goal/audience fork:** e.g. sell vs. inform vs. recruit; consumers vs. investors; if the topic doesn't say.
- **Language/region/locale** when ambiguous; **accessibility or device constraints** (kiosk, low-end phones).
- **Hosting/stack constraints:** must be React? existing repo? single file? CMS?
- **A genuine taste fork:** two or three directions that would produce *very different* sites and the topic does not
  decide between them (e.g. "calm editorial" vs "loud kinetic" for a music festival site).
- **Sensitive subject matter** (medical, legal, financial, political, religious, memorial): tone and claim limits.
- **Reference sites/styles they love or hate** - one optional question to capture taste.

## 4. Procedure
1. After reading the request, list unknowns and mark each `assume` or `ask` with the rule in section 1.
2. If no `ask` items -> state assumptions in <= 6 lines and build.
3. If `ask` items exist -> ask **before building**, in **one round**, **max 4 questions**, ordered by impact.
   Each question has 2-4 concrete options derived from this project, a recommended default, and an
   "You decide" choice. Say that unanswered questions will use the defaults.
4. Never ask about something you can infer, something trivially reversible, or something the user already said.
5. Do not ask permission to start, do not repeat a question the user skipped, and do not hold up work for a
   second round unless an answer reveals a new blocking unknown.

## 5. How to ask (format)
- If a tap-to-answer question tool exists in the environment (for example `ask_user_input_v0`), use it for choice
  questions, with a one-line lead-in.
- Otherwise use a short numbered list with lettered options and a marked default, e.g.
  `1) Direction: a) calm editorial b) loud kinetic c) cinematic dark (default c)`.
- Keep wording plain and concrete; describe options as *vivid one-line moods tied to the subject*, not labels like
  "Style A". No jargon.
- After sending questions, stop and wait for the reply (do not build in the same turn) - except when the user
  already said to proceed.

## 6. Question patterns (generate your own for the project)
- Taste fork, subject-specific: "For the roastery site, which feels more like you? a) a slow, warm farm-to-cup
  documentary b) a bold, graphic, sticker-and-type look c) a quiet, premium tasting-notes experience (default a)".
- Assets: "Do you have your logo, product photos, or brand colors? a) yes, I'll upload b) no, source/create them for me
  (default) c) I have some".
- Facts: "What name and tagline should I use, and what are the 3 main things you offer? (or 'make them up for now')".
- Goal: "What's the one action visitors should take? a) buy b) book a call c) follow/subscribe d) just be impressed".
- Reference: "Any site or brand whose look you love (or hate)? Paste a link or skip".
- Constraint: "Must it work as one file or inside a React project?".
Ask fewer, sharper questions; two good questions beat six mediocre ones.

## 7. Reading taste from what the user gives you
If the user supplies links, screenshots, sample prompts, or past work, **analyze the qualities** (type scale,
density, color world, motion temperament, media type, interaction style, how much copy) and write a 3-line taste
profile. Use it to steer the synthesis (`style-synthesis.md`). Do not clone the reference; extract principles.
The reference prompts in `taste-examples/` are examples of this kind of taste signal, not templates.

## 8. After the answers
Record a **User Taste Profile** (<= 6 lines: goals, tone, must-haves, dislikes, assets provided, constraints) and
pass it to style synthesis and the asset brief. Apply defaults for anything left unanswered. Briefly confirm the
plan in one or two lines, then build. Keep honoring the profile in later revisions.
