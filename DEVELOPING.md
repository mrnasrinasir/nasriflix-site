# Developing Nasriflix

This is the developer guide for the site. The goal: anyone (or any AI assistant) can pick this repo up cold and update it without extra context.

## TL;DR

- The **entire site is one self-contained file: `index.html`** (HTML + CSS + JavaScript, no build step, no dependencies).
- All talk/event content lives in a JavaScript array near the bottom of `index.html`.
- Images live in `assets/images/<slug>.jpg`.
- To change anything, **edit `index.html` directly and push to `main`** — Netlify auto-deploys in ~1 minute.

## Where the data lives

Inside `index.html` there are two key JS structures:

1. **`images`** — a map of `slug -> assets/images/<slug>.jpg`.
2. **`talks`** — the array of every card on the site. Each entry looks like:

```js
{
  name: "Talk title",
  slug: "media-mixer",          // must match the image filename
  sub: "Host / series",
  loc: "City, Country",
  role: "Speaker",
  date: "9 Jun 2026",
  featured: true,                 // shows in the Featured row + bigger card
  video: "fTYUW5d1LjQ",          // OPTIONAL single YouTube video ID
  playlist: "PLAxPBLJr9tB-...",  // OPTIONAL YouTube playlist ID
  channel: "https://www.youtube.com/@mrnasrinasir", // OPTIONAL
  link: "https://...",           // OPTIONAL external link
  desc: "Short one-line intro shown on the card and at the top of the pop-up.",
  covered: ["point", "point"],   // bullet list in the pop-up
  takeaways: ["point", "point"],
  outcome: "Closing line."
}
```

## Common updates

### Add a new talk/event
1. Add a `<slug>.jpg` image to `assets/images/`.
2. Add an entry to the `images` map: `"<slug>": "assets/images/<slug>.jpg"`.
3. Add a new object to the `talks` array with the fields above.

### Add a video to an existing talk
- For a single video: add `video: "<YOUTUBE_ID>"` to that talk's object. It will (a) embed in the pop-up and (b) show a muted, looping hover-to-autoplay preview on the card.
- For a playlist: add `playlist: "<PLAYLIST_ID>"` (and optionally `channel`). The full playlist plays inside the pop-up.

### Edit wording / sections / colours
- Talk copy: edit the relevant object in `talks`.
- Theme colours: the CSS variables at the top (`--red`, `--bg`, etc.).
- Section titles & footer: search the HTML for the heading text.

## YouTube embed patterns (used by the JS)

- **Hover preview (card):** `https://www.youtube-nocookie.com/embed/<ID>?autoplay=1&mute=1&controls=0&loop=1&playlist=<ID>&playsinline=1&modestbranding=1&rel=0`
- **Single video (pop-up):** `https://www.youtube-nocookie.com/embed/<ID>?rel=0`
- **Playlist (pop-up):** `https://www.youtube-nocookie.com/embed/videoseries?list=<PLAYLIST_ID>&rel=0`

The hover preview iframe uses `class="card-preview"` with `pointer-events:none` so clicking the card still opens the details pop-up.

## Deploy flow

1. Edit `index.html` (and/or add an image).
2. Commit & push to the `main` branch.
3. Netlify rebuilds automatically and the live site updates in ~1 minute: https://nasriflix.netlify.app/

## Optional: regenerating from a template

The site was originally produced from a template where the image map was a `__IMAGES_JSON__` placeholder, filled by this script. This is **optional** — editing `index.html` directly is the recommended path — but kept here for reference:

```python
import json, os

slugs = ["media-mixer","inside-notion","ai-labs","office-hour","network-school","openclaw","custom-agents-action","build-2026","wrap-party","youtube-meetup","notion-3","first-block"]
images = {s: f"assets/images/{s}.jpg" for s in slugs}

with open("template2.html", "r", encoding="utf-8") as f:
    html = f.read()

html = html.replace("__IMAGES_JSON__", json.dumps(images))

with open("index.html", "w", encoding="utf-8") as f:
    f.write(html)
```

## Current slugs (each has a matching image)

`media-mixer`, `inside-notion`, `ai-labs`, `office-hour`, `network-school`, `openclaw`, `custom-agents-action`, `build-2026`, `wrap-party`, `youtube-meetup`, `notion-3`, `first-block`
