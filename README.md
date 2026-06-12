# deck-skills

Two skills that turn any AI coding agent into a deck-making partner. One grills you until the brief is sharp. The other builds a single-file HTML deck, plus a PDF, that runs in any browser.

Built for people tired of AI-slop decks: tiny text, invented charts, fifty slides that say nothing.

## What's inside

- **prep-the-deck** — interviews you relentlessly, one question at a time, until the brief is locked. No deck gets built on a vague brief.
- **build-the-deck** — builds to a real quality bar: viewport-fitting, readable from the back of the room, real captured charts only (never invented graphs), hooked openers, verified rendering, and a clean PDF.

The full [frontend-slides](https://github.com/zarazhangrui/frontend-slides) engine is bundled inside `build-the-deck/engine/` (MIT), so one install gives you everything: the viewport-fitting base, 12 themes, animation patterns, PowerPoint import, and PDF export. No second download.

## Install

You need an AI coding agent (Claude Code, Cursor, Codex, or similar). Pick whichever option fits your setup.

### Option A — one-line installer (easiest)

Needs Node installed. Works across most agents:

```bash
npx skills@latest add mattburnsgg/deck-skills
```

Select both skills when prompted, then restart your agent.

### Option B — Claude Code plugin

In Claude Code, add this repo as a plugin marketplace, then install it:

```
/plugin marketplace add mattburnsgg/deck-skills
/plugin install deck-skills
```

### Option C — manual (works with any agent)

Clone the repo and copy the two skill folders into your agent's skills directory:

```bash
git clone https://github.com/mattburnsgg/deck-skills.git
cp -r deck-skills/skills/prep-the-deck   ~/.claude/skills/
cp -r deck-skills/skills/build-the-deck  ~/.claude/skills/
```

The Claude Code skills directory is `~/.claude/skills/` on macOS and Linux, and `%USERPROFILE%\.claude\skills\` on Windows. Adjust the path for other agents.

Once installed, paste the prompt below.

## Use it

Paste this to your agent (also in [PROMPT.md](./PROMPT.md)):

> Build me a slide deck about [your topic].
>
> First, use prep-the-deck. Grill me relentlessly, one question at a time, with a recommended answer each time, until the brief is locked. Do not start building until the brief is locked.
>
> Then use build-the-deck to produce a single-file HTML deck that runs in any browser, plus a PDF.
>
> Hard rules: never invent a chart or a graph. Use only real data you can capture from a source, or a big number with a citation. Every slide has to be readable from the back of a room.

Answer the questions. Pick your cover. Get a deck.

## Why the grilling matters

Most decks fail before a single slide is designed, because nobody pinned down the one outcome, the audience, or the thesis. prep-the-deck refuses to start until those are locked. It is annoying on purpose. It saves you the three rebuilds.

## Built on

- The **frontend-slides** engine, vendored into `skills/build-the-deck/engine/` (MIT, by zarazhangrui), for the single-file HTML mechanics, viewport fitting, themes, and PowerPoint import: https://github.com/zarazhangrui/frontend-slides
- The **grill** pattern from Matt Pocock's skills: https://github.com/mattpocock/skills

## Make them your own

These are small and easy to adapt. Every rule in `build-the-deck/QUALITY.md` came from a deck that shipped, drew a note, and taught a lesson. When you learn a new one, add it. That is how the deck-making gets better.

## License

MIT. See [LICENSE](./LICENSE).
