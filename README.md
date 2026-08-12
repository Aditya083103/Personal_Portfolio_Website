# Portfolio

## Structure

```
Portfolio Website/
├── index.html          (home page)
├── AIRP.dc.html
├── Baggage-Claim.dc.html
├── Voice-Chatbot.dc.html
├── Beyond.dc.html
├── Arcade.dc.html
├── support.js                 (Claude-Design runtime, generated — do not edit by hand)
├── image-slot.js              (drag-and-drop image component)
├── .image-slots.state.json    (image-slot sidecar — persisted drop state)
├── headshot.jpg
├── assets/
│   ├── docs/
│   │   └── Resume_Aditya_Bhavsar.pdf
│   ├── images/
│   │   ├── favicon/
│   │   └── og/
│   └── videos/
```

### Why the pages stay at the project root

`image-slot.js` persists dropped images to `.image-slots.state.json` via a
sidecar file that the Claude-Design host bridge only allows writing **at the
project root** — the component's own doc comment states this explicitly.
`image-slot.js` also fetches that sidecar with a root-relative path.

`index.html` (headshot) and `Beyond.dc.html` (4 photos) both use
`<image-slot>`, and `support.js`/`image-slot.js` are loaded via `./support.js`
relative script tags. Moving those pages into a `pages/` subfolder would break
sidecar reads/writes and the relative script includes. Given that risk, all
`.dc.html` pages and the two runtime scripts stay at the root, and only
content/reference assets (resume, videos, favicons, OG images) are organized
into `assets/`.

## Local preview

Serve the folder root with any static file server, e.g.:

```bash
npx serve .
```

Open `index.html` (or whichever page you're working on) from the
served root — opening via `file://` breaks the `.image-slots.state.json`
fetch and the `<image-slot>` drop feature.

## Updating the resume

Replace `assets/docs/Resume_Aditya_Bhavsar.pdf` with the new file, keeping
the same filename — all "Resume" / "Download résumé" links on the site point
to that path.

## Updating the AIRP demo videos

Drop the files in at these exact paths — the AIRP page will pick them up
automatically once they exist:

- `assets/videos/airp-hero-demo.mp4` + `assets/videos/airp-hero-poster.jpg`
- `assets/videos/airp-deep-dive.mp4` + `assets/videos/airp-deep-dive-poster.jpg`

Until then, the page shows a poster image with a "Demo video coming soon" badge.
