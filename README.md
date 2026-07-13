# Happy Birthday, Richi 🎂

A single-page, cinematic birthday experience: candle → cake → blown-out wish →
celebration → photo gallery → letter → video → fireworks → gift box.

No build step. No framework. It's one HTML file with embedded CSS and
JavaScript, plus a few CDN libraries (GSAP for animation timing and
canvas-confetti for the confetti burst). Open it and it works.

## 1. Run it locally

Just double-click `index.html` — it opens in your browser and works.

The only catch: the microphone "blow out the candle" feature and loading
your own photos/video/audio require the page to be served over `http://`
or `https://` (browsers block microphone access and some file loading on
`file://`). To get the full experience while testing, run a tiny local
server from this folder:

```bash
# Python 3
python3 -m http.server 8080

# or Node
npx serve .
```

Then open `http://localhost:8080`.

## 2. Personalise it

Open `index.html` in a text editor and look for the `CONFIG` block near the
top of the `<script>` section:

```js
const WIFE_NAME = "Richi";
const LETTER_TEXT = `My darling ${WIFE_NAME}, ...`;
const PHOTO_LIST = [
  { src: "assets/images/photo-1.jpg", caption: "the beginning" },
  ...
];
```

- **Name** — change `WIFE_NAME`.
- **Letter** — rewrite `LETTER_TEXT`. It supports line breaks; it will type
  itself out automatically.
- **Photos** — drop your images into `assets/images/` (any filenames you
  like) and update `PHOTO_LIST` to match. Add or remove entries freely —
  the gallery grid adapts to however many you give it.
- **Music** — replace `assets/audio/piano.mp3` with any MP3 of your
  choosing (same filename, or update the `<source>` path in the `<audio>`
  tag near the bottom of the HTML).
- **Video** — replace `assets/video/message.mp4` with your own video (same
  filename, or update the `<source>` path in the video section). Until you
  add a real file, that section shows a friendly placeholder instead of a
  broken player.

All of the SVG artwork (candle, flame, cake, gift box) is hand-drawn in the
HTML itself — no external image assets required for those.

## 3. How the "blow out the candle" moment works

When the candle scene reaches "Make a wish," the page asks for microphone
permission. If granted, it listens for a burst of breath noise and
extinguishes the flame when detected. If the person denies permission, has
no microphone, or nothing is detected within a few seconds, the flame
extinguishes automatically — nobody gets stuck.

## 4. Deploy it

### Vercel
1. Push this folder to a GitHub repository.
2. Go to [vercel.com/new](https://vercel.com/new), import the repo.
3. Framework preset: **Other** (it's static HTML, no build command needed).
4. Deploy. Done.

Or skip GitHub entirely with the Vercel CLI:
```bash
npm i -g vercel
vercel
```

### GitHub Pages
1. Push this folder to a GitHub repository.
2. In the repo, go to **Settings → Pages**.
3. Under "Build and deployment," set **Source** to `Deploy from a branch`,
   branch `main`, folder `/ (root)`.
4. Save. Your site will be live at
   `https://<your-username>.github.io/<repo-name>/` within a minute or two.

### Netlify
Drag the whole folder onto [app.netlify.com/drop](https://app.netlify.com/drop).
That's the entire deployment.

## 5. Project structure

```
birthday/
├── index.html            everything: markup, styles, animation logic
├── assets/
│   ├── images/            your photos for the gallery (photo-1.jpg ...)
│   ├── audio/              piano.mp3 — background music
│   └── video/              message.mp4 — the video message
└── README.md
```

## 6. A note on scope

This was built as one polished, dependency-free HTML file rather than a
full Next.js/TypeScript project, on purpose: it means zero install steps,
zero build errors, and zero risk of half-wired imports — you can open it
today and it just works, on any static host. If you'd ever like it ported
into a Next.js codebase (e.g. to add a CMS, multi-page routing, or a build
pipeline), that's a very doable follow-up — just ask.
