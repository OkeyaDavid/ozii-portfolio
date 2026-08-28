# OZII — Creator Portfolio

A portfolio site for a Toronto-based fashion & lifestyle creator and short-form
video editor. Built as a single hand-written HTML file with no framework, no
build step and no dependencies.

**Live:** https://okeyadavid.github.io/ozii-portfolio/

<!-- Add a screenshot: press Cmd+Shift+4 on the hero, save it as
     docs/preview.png, then uncomment the line below.
![Screenshot of the site](docs/preview.png)
-->

---

## What it does

**Click-to-play work index.** The projects are a typographic list rather than a
grid. Hovering a row sweeps a fill across it and floats a preview card that
chases the cursor with easing and tilts based on pointer velocity. Clicking
opens a full-screen player with audio.

**Audio that actually plays.** Browsers block unmuted autoplay, so playback is
started from the click itself — which counts as a user gesture. If a browser
refuses anyway, it falls back to muted and surfaces an unmute control rather
than playing silently.

**Scroll-reactive motion.** Two marquee bands drift continuously and change
speed and direction based on scroll velocity. Headlines are split into
line-masks that swing up in sequence. Portraits parallax inside their frames.

**Custom cursor.** A trailing ring that swells into a labelled disc over
interactive elements, and inverts its colours over the light section.

**A deliberate contrast flip.** The rates section switches the entire page from
near-black to bone with dark type, as a mid-scroll break.

## Performance

The media was the whole problem. Source assets totalled **161 MB**, including a
24 MB PNG used as a 300px-wide hover thumbnail and a 19-second clip exported at
4K/32 Mbps.

| | Before | After |
|---|---:|---:|
| Images | 34.6 MB | 350 KB |
| Video | 126.6 MB | 26.0 MB |
| **Images loaded on page open** | **35 MB** | **0 KB** |

Preview images are no longer created upfront — each one is fetched the first
time its row is hovered, with a typographic plate standing in until it lands.

## Accessibility & robustness

- Every animation is disabled under `prefers-reduced-motion`
- The lightbox traps focus, closes on `Esc`, and navigates with arrow keys
- Touch devices get a real grid instead of the hover index, since there is no
  hover to reveal with
- Project rows with no clip yet show a fallback panel instead of an empty player

## Stack

Vanilla HTML, CSS and JavaScript. Google Fonts (Bodoni Moda, Archivo, DM Mono).
`IntersectionObserver` for reveals and counters, a single `requestAnimationFrame`
loop for all scroll-driven motion, and `<canvas>` for the film-grain overlay.

## Structure

```
index.html            everything — markup, styles, script
img/
  preview-*.webp      work thumbnails (hover previews)
  logo-*.webp         client logos
  ozii-*.webp         portraits
video/
  clip-*.mp4          project clips, 1080×1920 H.264 + AAC
Ozii_Rate_Card.pdf    downloadable rate card
```

## Running it locally

No build step — open `index.html` in a browser.

For live reload while editing, use the **Live Server** extension in VS Code
(right-click `index.html` → "Open with Live Server").

## Adding a project

1. Export the clip vertical (1080×1920), H.264 + AAC, ideally under 10 MB
2. Save it as `video/clip-<name>.mp4` and a thumbnail as `img/preview-<name>.webp`
3. On that row in the SELECTED WORK section, set `data-video` and `data-img`,
   and remove `data-empty`

The filename prefixes matter — `.gitignore` uses them to decide what ships.

## Deploying

Hosted on GitHub Pages, deployed from `main`. Pushing to `main` publishes.

---

© Ozii. Code is MIT; photography, video and brand assets are not licensed for reuse.
