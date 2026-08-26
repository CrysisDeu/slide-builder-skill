---
name: slide-builder
description: Build presentation slide decks that tell a story. Use when the user asks to create slides, a deck, a presentation, workshop slides, or a pitch deck. Enforces a story-first workflow (lock the script before building slides), the Why/What/How framework, large text, and image-led slides.
triggers: create slides, build a deck, slide deck, presentation, workshop slides, pitch deck, make slides, talk
version: 1.0.0
---

# Slide Builder

Build decks that tell a story and pull the audience in. A slide deck is NOT the presentation — it is the visual anchor for a story the presenter tells. Get the story right first; the slides come last.

## The workflow (do these in order — do not skip)

### Phase 0 — Ask the style first
Before building anything, ask the user what visual style they want, and show options to aid the choice.
- Ask: audience, setting (room size / screen), tone, and any reference deck they like.
- Offer 2-3 concrete style directions (e.g. dark + bold accent, light editorial, minimal mono). If you can, show a small visual sample of each before they pick.
- If the user gives a reference deck, read it and name the specific structural moves you'll reuse.
- **Layout templates** live in `templates/` (20 HTML files, one per layout type). These illustrate **structure only** — the colors, fonts, and visual treatment should be customized for each deck based on the user's chosen style. Read `references/slide-layouts.md` for the full catalog and decision table.

### Phase 1 — Lock the story BEFORE slides
Write a flow/script doc (markdown) and align on it before opening an HTML file.
- The doc holds the FULL narrative: the thesis, the arc, what each slide says, and the spoken talking points.
- Get the argument right here. Slides built on a weak story can't be saved by visuals.
- Confirm the thesis and arc with the user before moving on.

### Phase 2 — Build the slides as anchors
Only after the script is locked, build the deck. Each slide carries one beat of the story — it is not a transcript.

### Phase 3 — Fresh-eye review via subagent
After edits are done, spawn a subagent with this prompt to get an independent critique:

> You are an expert presentation designer. Critique these slides — be specific. For each slide: call out what works and what doesn't; suggest changes that would make the slide clearer and more visually appealing. Focus on: text density (too much reading?), font readability from the back of a room, visual hierarchy, whether the headline carries the point alone, and pacing across the full deck.

Read the subagent's feedback, fix what's valid, and discard what conflicts with the locked story.

## Entertain your audience (the real goal)

The goal of a presentation is to entertain, not to inform. An informed audience forgets in a day. An entertained audience tells their friends.

- **Stories over facts.** Open each section with a concrete anecdote ("I left at 5, my agent fixed a SEV-2 at 3am"). Data backs up the story; it never replaces it.
- **Surprises.** Each slide should land one thing the audience didn't expect. If they can predict what's next, you've lost them.
- **Tension and release.** Make the problem slide hurt. Make the product slides feel like relief.
- **Humor where natural.** People remember talks they laughed during. Don't force it, but don't be dry.
- **Vary the pacing.** Big number → quiet story → screenshot → punchline. Monotone information delivery is the enemy.

A slide that *informs* says "The tool has scheduled jobs, background workers, and sub-agents." A slide that *entertains* says "I went to bed. My agent filed the fix, got it reviewed, and shipped it before my alarm went off."

**But back it up.** Entertaining does not mean fabricating. Every story or claim on a slide must be something that actually happened, with data you can point to if asked. If you don't have a real anecdote, don't invent one — ask the user for one or use a verified metric instead. An audience that catches a made-up story trusts nothing else in the deck.

## Tell a story (rule 1 + 2)

Every deck is one argument, not a feature list. The audience should be pulled in.

**Why / What / How** is the backbone:
- **Why** — open with the problem and the stakes. Make them care before you explain anything.
- **What** — what the thing is, in one breath.
- **How** — how it works / how they use it.

Storytelling moves that work:
- **Contrarian or provocative title** — state a claim worth arguing with, not a logo. ("Most X do Y — we don't.")
- **Name the hard problem sharply** — one slide that makes the tension felt, with a crisp insight.
- **Build toward one thesis** — every slide earns the next; end each section with a handoff line.
- **Make the audience the protagonist** — land the close on them ("you walk in X, you leave Y").
- Metrics and credibility punctuate the argument; they never open it.

Anti-pattern: a **feature tour** (slide after slide of "we also have X"). It has no spine and no one remembers it. If your deck is a list, it's weak — rebuild the structure, don't polish the fonts.

## Large text (rule 3)

No one reads small text — and the presenter shouldn't be reading the slide either.
- Headlines large enough to read from the back of the room (think ~40pt+; in self-contained HTML use `clamp()` with container queries so it scales).
- One idea per slide. If you need to read it, there's too much on it.
- Talking points, NOT full sentences. The slide is not a teleprompter.
- **Chekhov's gun:** if something is on the slide, it must matter. If it's too small for the audience to read, it's either important enough to make bigger or it shouldn't be there at all. No decorative small text.

## Use images, big (rule 4)

Lead with visuals. Words support the image, not the other way around.
- Use many screenshots/diagrams. If an image isn't available, insert a clearly-marked **placeholder** and **ask the user to screenshot it** — never fabricate or describe a screenshot you don't have.
- Make images readable: large by default. **If an image is the only thing on a slide, it fills the slide** — maximize width/height (`object-fit: contain`, near-full viewport).
- Use an image only if it actually shows what the slide claims. A loosely related screenshot (e.g. a "rich output" shot standing in for "the chat interface") is the wrong image — use a placeholder instead.
- For split slides: image ~60%, text ~40%.
- **Respect image aspect ratio.** Don't force a wide screenshot into a tall container (or vice versa) — it leaves dead space and shrinks the image. Check the actual dimensions of images before choosing the layout. Ultra-wide images (banners, notifications) should span full width in a stacked layout, not sit inside a portrait-oriented split box.

## Data on a slide

A chart is a sentence, not a spreadsheet. The skill already says "use Chart.js" — this is how to make the chart land.

- **One chart, one message, stated in the headline.** The takeaway goes in the slide title ("Usage tripled after launch"), not left for the audience to infer. Same assertion-evidence rule as text slides.
- **Mark the point with one pre-attentive cue.** Size, color, and position register before conscious attention. Color the one bar/line that carries the argument; everything else stays neutral gray. One accent, not a rainbow.
- **Declutter.** Remove gridlines, chart borders, 3D, drop shadows, dual axes, and heavy tick labels. Every pixel that is not the data is noise (Tufte's data-ink ratio).
- **Label directly, drop the legend.** Put the series name at the end of its line or on its bar. A legend forces the eye to ping-pong; direct labels also read better for colorblind viewers. One series needs no legend at all.
- **Round the numbers.** "15M" not "15,283,401." Do not make the room do arithmetic.
- Group with intent: items placed near each other read as related (proximity), items that look alike read as a set (similarity). Use that to structure the chart, not decoration.

Sources: Knaflic, *Storytelling with Data* (declutter, focus, one message); Tufte, *The Visual Display of Quantitative Information* (data-ink, chartjunk); pre-attentive attributes and Gestalt grouping (Healey/Ware; Gestalt principles).

## Slide-craft rules

- **Self-contained HTML, no CDN.** Inline CSS only. It must render correctly opened as a local file, offline. (No `cdn.tailwindcss.com`, no external scripts.) **Exceptions:** Chart.js and Anime.js from cdn.jsdelivr.net are acceptable — Chart.js for data visualization, Anime.js for sequenced animations (count-ups, staggered reveals, flywheel rotation). Use these over hand-rolled CSS keyframes for anything non-trivial.
- **Diagrams: never ASCII / box-drawing art.** In a no-CDN deck, build diagrams with styled HTML boxes or inline SVG. (Mermaid needs a CDN — use Mermaid only in markdown docs, not in the deck.)
- **Responsive scaling:** wrap each slide in a `container-type: size` element and size text with `clamp(min, Ncqw, max)` so the deck scales to any screen.
- **No emojis** in professional decks unless the user's chosen reference style uses them.
- Keep navigation simple (arrow keys + prev/next buttons + slide counter).

## Verify before you assert

If a slide makes a factual or architectural claim, confirm it against the real source (code, data, docs) before drawing it. A claim that looks good but is false ("thin core" when the core is 90K lines) gets called out by the first expert in the room. Be honest when the evidence kills a nice-sounding line.

## Don't over-edit

When the user asks for a targeted change, make ONLY that change. Do not restructure a diagram or rewrite a section they didn't ask about. Preserve everything they liked.

## Title slide

Keep the opening slide calm and conventional: a short title, an optional one-line subtitle, the presenters, and the occasion + date. Do NOT put the thesis or the hook on the title slide — that punch belongs on the problem slide a few slides in. A title slide that shouts the argument feels off.

## Every slide earns a title and stands alone

- Every content slide needs a clear, legible title — a real heading, not just a small kicker or label. The audience should know what the slide is about at a glance.
- Each slide must make sense on its own as the talk moves forward. Name the subject on the slide; avoid pronouns like "it" that point at something the audience hasn't been shown yet (e.g. an agenda that says "what it does for you" before the product is even named).

## Write like a human (avoid AI tells)

A person reads these slides aloud — copy that sounds machine-generated undercuts them. Avoid the antithesis constructions that read as AI-generated:
- "X is the A, not the B"
- "it isn't X, it's Y"
- "not just X, but Y"
- the em-dash "— not the ..." reversal

Write plain declarative sentences instead. Also cut hype filler ("game-changer", "seamless", "unlock", "revolutionize", "supercharge").

When a concept gets corrected while you build, replace it outright with the correct version. Do not keep the original wording and bolt on a "not X, but Y" correction. The slide is a standalone artifact the audience reads cold — they never saw the chat. Present the final concept directly, as if it were always the answer.

## Research-backed frameworks (why these rules work)

- **Assertion-Evidence (Michael Alley, Penn State).** Every slide = a full-sentence *assertion* headline that states the takeaway (not a topic label like "Results" or "Architecture"), supported by *visual evidence* — a diagram, photo, chart — not a bullet list. Shown in controlled studies to improve audience comprehension, recall, and the speaker's credibility. Practical rule: write each headline as a complete sentence stating the point.
- **One Big Idea + audience as hero (Nancy Duarte, _Resonate_).** Filter everything through one key message; cut whatever doesn't support it. The audience — not you — is the protagonist. Structure as a story with a clear beginning/middle/end and use the "what is → what could be" contrast to create tension. Never build "slideuments" (dense docs masquerading as slides).
- **Signal-to-noise ratio (Garr Reynolds, _Presentation Zen_).** Maximize signal, strip noise: dense text, redundant bullets, distracting animation, decorative clutter, logos on every slide. Principles: restraint, simplicity, naturalness.
- **10/20/30 (Guy Kawasaki).** ~10 slides, ~20 minutes, 30-point minimum font. The font floor is the real lesson — it physically forces you to keep only the essential words and stops you from reading the slide aloud.
- **Redundancy principle (Mayer, Cognitive Theory of Multimedia Learning).** People learn better from visuals + spoken words than from visuals + speech + on-screen text (supported in 16/16 experiments, median effect size 0.86). So: narrate the detail, don't print your script on the slide. Place labels next to the graphic they describe (spatial-contiguity principle).

These five independently arrive at the same place: **one idea per slide, a sentence that states the point, a visual that proves it, and the words come out of the presenter's mouth — not off the slide.**

## Quick checklist before you ship a deck

- [ ] **Final fresh-eye review done** — after edits are complete, re-read the entire deck start to finish as if seeing it for the first time. Editing one slide often makes adjacent slides redundant, inconsistent, or out of order. Catch that before presenting.
- [ ] Style confirmed with the user (Phase 0)
- [ ] Story/script locked and aligned (Phase 1)
- [ ] One argument, Why → What → How, builds to a thesis
- [ ] One idea per slide, text large enough for the back row
- [ ] Image-led; placeholders flagged for any missing screenshots (and no wrong/loosely-related image used as filler)
- [ ] Every slide has a clear title; no pronoun pointing at something not yet shown
- [ ] Self-contained HTML, no CDN, no ASCII diagrams
- [ ] Every factual/architecture claim verified
- [ ] Title slide is conventional (title, subtitle, authors, occasion/date) — thesis lives later
- [ ] Copy reads human — no "X, not Y" antithesis, no hype filler
