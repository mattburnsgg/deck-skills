---
name: build-the-deck
description: Build a great single-file HTML slide deck from a locked brief. Wraps the frontend-slides engine and enforces the quality rules that separate a real deck from AI slop: viewport-fitting, a legibility floor, real captured charts only, hooked openers, verified rendering, and a clean PDF. Use after prep-the-deck, or whenever someone wants an actual deck built.
---

Build the deck from the locked brief. If there is no brief, run `prep-the-deck` first. Output is one self-contained HTML file that runs in any browser, plus a PDF.

## Step 0 — load the engine
Use the **frontend-slides** engine for the mechanics: zero-dependency single-file HTML, the viewport-fitting law (every slide is 100vh, no in-slide scroll, clamp everything), anti-AI-slop motion, and PowerPoint import. Read [ENGINE.md](./ENGINE.md). Repo: https://github.com/zarazhangrui/frontend-slides

## Step 1 — hook the openers
Treat the cover and every section opener as a hook. Draft 3-5 options each, pick the sharpest, write the rest of the slide downstream of it. A label like "Section 2" or "Our Data" wastes the slot. A strong cover on an average deck beats a weak cover on a strong deck.

## Step 2 — build to the quality bar
Read [QUALITY.md](./QUALITY.md) and follow it. The short version:
- **One idea per slide.** If you cannot name the slide in five words, it has two ideas.
- **Legibility floor.** Body text never below ~24px, captions never below ~18px. Readable from the back of the room. This is the rule that gets violated most.
- **Real captured charts and cards only.** Never hand-draw a graph. A slide shows either a real chart captured from a source, or a big number with a citation. QUALITY.md has the capture technique.
- **Separate regions** for text and visuals. No text dumped over a busy chart.
- **Animate with intent.** Slow, one element per slide, respect reduced-motion.
- **Close on a question or a next action.** Never a "thank you" slide.

## Step 3 — multi-variant the cover
Ship 3 cover treatments labeled A, B, C. Let the user pick, then strip the rest.

## Step 4 — verify before you hand it over
Do not claim it works until you have checked. Verify by measurement (QUALITY.md section 6): every slide fits 100vh with no content overflow, every type size meets the floor, arrow-key nav works. Then export the PDF (QUALITY.md section 7).

Build to completion. Decide the rules, surface the real choices, and push to a finished deck.
