# Quality bar for great decks

The rules that separate a real deck from AI slop. Most came from a deck that shipped, drew a complaint, and taught a lesson. Follow them.

## 1. One idea per slide
If you cannot name the slide in five words, it has two ideas. Split it. Spare slides and many of them beats dense slides and few of them.

## 2. The legibility floor (the most-violated rule)
A deck is read from the back of a room.
- Body text never below ~24px. Captions never below ~18px.
- Cramming is what forces small type. The fix for "too small" is less on the slide, not a smaller font.
- Do not trust an auto-fit that scales type down to make content fit. Cut content instead.

Verify it with measurement (section 6).

## 3. Real captured charts only. Never hand-draw a graph.
Hand-built bar and pie charts get the scaling wrong and read as incorrect. They also look fake. Two allowed visuals for data:
- a **real chart captured from the source**, or
- a **big number with a citation**.

Never a hand-drawn graph. Never show a recreated chart and the real chart of the same data side by side.

### Capturing a real source chart
Most research blogs serve their charts as static images on a CDN. You do not need a screenshot tool.
1. Fetch the article HTML with a real browser User-Agent.
2. Pull the chart image URLs out of the `<img src>` tags. Filter out avatars and logos (drop names containing `120x120`, `author`, `avatar`, `logo`).
3. Download the chart straight to your images folder.
4. Validate it is a real image by checking the magic bytes. PNG starts with `89 50 4E 47`. JPEG starts with `FF D8 FF`. A tiny file is usually an HTML error page wearing a `.png` name.
5. Open it and confirm it is the RIGHT chart. Watch for a chart that proves the opposite of your point (a "schema correlates with citations" chart undercuts a "schema does nothing" slide).

You get a pristine, full-resolution chart with no cursor and no flaky capture step.

### If you are ever forced to draw a bar
Its width equals its value on a real axis. A 15% value draws as 15% of the track, never relative to the biggest bar. A "15%" bar drawn full-width is the classic tell that the chart is fake. But prefer a real chart.

## 4. Text and visuals get their own regions
Primary text in one region, the visual in another. No text dumped over a busy chart without a scrim behind it.

## 5. Hooks, not labels
The cover and every section opener is a hook. Draft 3-5 and pick the sharpest. A label ("Section 2", "Our Data", "Agenda") wastes the slot and the attention.

## 6. Verify by measurement, not by vibes
Screenshot tools can be flaky. Confirm the deck is sound by measuring it in a headless or preview browser:

```js
// overflow check: any slide whose content spills its 100vh box
[...document.querySelectorAll('.slide')].forEach((el, i) => {
  if (el.scrollHeight > el.clientHeight + 2) console.log('overflow on slide', i);
});

// legibility check: read computed font sizes and confirm they meet the floor
const px = sel => parseFloat(getComputedStyle(document.querySelector(sel)).fontSize);
console.log('body', px('.body'), 'caption', px('.caption'));
```

Pass when every slide fits with no content overflow, every type size meets the floor, and arrow-key nav works.

## 7. Ship a clean PDF
Add a print stylesheet so each slide is one landscape page:

```css
@page { size: 1280px 720px; margin: 0; }
@media print {
  html { scroll-snap-type: none; height: auto; overflow: visible; }
  body { height: auto; overflow: visible; }
  .slide { height: 720px; width: 1280px; page-break-after: always; overflow: hidden; }
  .slide:last-child { page-break-after: auto; }
}
```

Then print to PDF with headless Chrome:

```bash
chrome --headless=new --no-pdf-header-footer --virtual-time-budget=10000 \
  --print-to-pdf="deck.pdf" "file:///path/to/deck.html"
```

## 8. Close on a question or a next action
Never a "thank you" slide. Leave the audience with something to carry out of the room.

## 9. Cover variants
Ship 3 cover treatments labeled A, B, C. Let the user pick, then strip the rest before final.
