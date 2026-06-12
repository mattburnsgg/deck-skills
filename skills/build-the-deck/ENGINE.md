# The engine: frontend-slides

The mechanics come from the frontend-slides engine. Repo: https://github.com/zarazhangrui/frontend-slides

Install it as a plugin, or read these files from it and fold them into your deck:
- `viewport-base.css` — the viewport-fitting base. Locks html and body to the viewport, makes every `.slide` 100vh (and 100dvh), and sets `overflow: hidden` so nothing spills. One change: raise its type floors to meet the legibility bar in QUALITY.md. Its defaults run small.
- `html-template.md` — base document structure.
- `animation-patterns.md` — entrance and transition motion.
- `scripts/extract-pptx.py` — import an existing PowerPoint.
- `scripts/export-pdf.sh` — a PDF export helper.

## The non-negotiable: viewport fitting
Every slide is exactly one viewport tall, with no internal scroll. Build each slide to fit at large type. If it does not fit, cut content. Do not shrink the font.

## Minimal nav (vanilla JS, no dependencies)
Arrow keys plus scroll-snap, and a fade-up on the active slide:

```js
const slides = [...document.querySelectorAll('.slide')];
let i = 0;
addEventListener('keydown', e => {
  if (['ArrowRight','ArrowDown',' '].includes(e.key)) {
    e.preventDefault(); i = Math.min(slides.length - 1, i + 1);
    slides[i].scrollIntoView({ behavior: 'smooth' });
  } else if (['ArrowLeft','ArrowUp'].includes(e.key)) {
    e.preventDefault(); i = Math.max(0, i - 1);
    slides[i].scrollIntoView({ behavior: 'smooth' });
  }
});
const obs = new IntersectionObserver(
  es => es.forEach(en => { if (en.isIntersecting) en.target.classList.add('active'); }),
  { threshold: 0.55 }
);
slides.forEach(s => obs.observe(s));
```

## Scroll container
Put the scroll container and the scroll-snap on the SAME element (the `<html>` element), or programmatic scrolling fights the snap:

```css
html { height: 100%; overflow-y: scroll; scroll-snap-type: y mandatory; scroll-behavior: smooth; }
body { min-height: 100%; }
.slide { height: 100vh; height: 100dvh; scroll-snap-align: start; overflow: hidden; }
```

Keep it tiny. The whole deck is one HTML file with one font CDN call and nothing else.
