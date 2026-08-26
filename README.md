# slide-builder

An agent skill for building presentation decks that tell a story — not feature tours, not documents projected on a wall.

Works with any agent that reads `SKILL.md`-style skills (Claude Code, Kiro, Cursor, skills.sh, etc.).

## What it enforces

- **Story before slides.** Lock a written script and the thesis first; the HTML comes last. Slides built on a weak argument can't be saved by visuals.
- **Entertain, then inform.** An informed audience forgets in a day. Real stories backed by real data, never fabricated anecdotes.
- **Why / What / How** spine, with a single thesis the whole deck serves.
- **Big text, image-led slides.** If it's too small to read from the back of the room, cut it or say it aloud.
- **Fresh-eye review.** A sub-agent critiques the finished deck before you present it.

It also carries the research behind the rules — assertion-evidence headlines, Duarte / Reynolds / Kawasaki, data-on-a-slide (Knaflic, Tufte), cognitive load (Cowan 4±1, Sweller, Mayer), opening hooks, serial-position closings, pacing, and WCAG 2.2 / colorblind / projector accessibility.

## Layout templates

`templates/` holds 20 self-contained HTML layouts, one per slide type:

| | | |
|---|---|---|
| 01 title | 08 list | 15 demo placeholder |
| 02 statement | 09 quote | 16 team |
| 03 split text + image | 10 definition table | 17 agenda |
| 04 full-bleed image | 11 before / after | 18 call to action |
| 05 metrics | 12 timeline | 19 two images |
| 06 chart | 13 two-column comparison | 20 quote + image |
| 07 diagram | 14 icon grid | |

They illustrate **structure only** — restyle colors and type per deck. See `references/slide-layouts.md` for the decision table on which layout fits which beat.

## Install

Clone into your agent's skills directory:

```bash
# Claude Code
git clone https://github.com/CrysisDeu/slide-builder-skill ~/.claude/skills/slide-builder

# Kiro Crew
git clone https://github.com/CrysisDeu/slide-builder-skill ~/.kiro/crew/skills/slide-builder
```

Then ask your agent to "build a deck about X" and it will pick the skill up.

## Layout

```
SKILL.md                      the workflow and rules
references/slide-layouts.md   layout catalog + decision table
references/minto-pyramid.md   structuring the argument
templates/*.html              20 layout templates
```

## License

MIT
