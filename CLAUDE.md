# ದಯೆ ಇರಲಿ · Daye Irali

A single-page, bilingual (Kannada/English) site for an environmental movement.
Tagline: **ಪರಿಸರದ ಮೇಲೆ ದಯೆ ಇರಲಿ** — "Let there be compassion for nature."

## Structure

Everything lives in `index.html` — markup, CSS and JS inline, no build step, no
dependencies beyond Google Fonts (Baloo Tamma 2, Noto Sans Kannada).

```
index.html            the whole site
logo.png              full logo artwork (hero)
favicon.png           centre crop of the logo (nav, footer, favicon)
apple-touch-icon.png  180x180, generated from favicon.png
```

Sections in order: hero → why (air/water/soil/life) → Basavanna quote → pledge
checklist → how-it-grows steps → closing → footer.

### Bilingual mechanism

`<body data-lang="kn|en|both">` plus `.kn` / `.en` classes on every text node.
CSS hides the inactive language; the choice persists in `localStorage` under
`di-lang`. Pledge checkbox state persists under `di-pledges`.

**When adding copy, always add both a `.kn` and an `.en` variant.** A string with
only one will show in "both" mode but vanish in the other.

### Colours

Defined as CSS custom properties on `:root`, with a dark-mode override under both
`prefers-color-scheme: dark` and `:root[data-theme="dark"]`. Key ones: `--deep`
(#0D3B2A hero green), `--turmeric` (#F2A33A accent), `--leaf`, `--bg`, `--ink`.

## Logo

The logo is the client's own supplied artwork, used as a **raster image**. Do not
replace it with hand-drawn SVG — that was tried twice and rejected. The white disc
is baked into the PNG; `border-radius:50%` in CSS rounds it against the dark hero.

`favicon.png` is a centre crop of just the globe, hands and tree, because the full
ring and Kannada wordmark are illegible below ~64px.

## Deployment

- GitHub: `wishiknew/daye-irali` (private), branch `main`
- Live: https://daye-irali.onrender.com/ — Render Static Site, auto-deploys on
  push to `main`. Build Command empty, Publish Directory `.`

### Git identity for this repo

Two GitHub accounts exist on this machine, wired as SSH aliases in `~/.ssh/config`:

| alias | account | use |
|---|---|---|
| `wishiknew` | `wishiknew` | **this project** (personal) |
| `pravar` | `vishnutej-pravar` | work; also what the `gh` CLI is logged into |

This repo is configured locally with `user.name=wishiknew` and
`user.email=wishiknew@users.noreply.github.com`; the remote is
`wishiknew:wishiknew/daye-irali.git`. Global git identity is unset.

**Do not use the `gh` CLI here** — it authenticates as the work account. Create
repos through the browser instead, or via a separate config dir
(`gh-personal` alias in `~/.zshrc` points `GH_CONFIG_DIR` at `~/.config/gh-personal`,
though that account has not been logged in yet).

## Working notes

- Verify visual changes by rendering, don't assume:
  ```
  "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless \
    --disable-gpu --screenshot=out.png --window-size=1200,800 --hide-scrollbars \
    "file://$PWD/index.html"
  ```
  `rsvg-convert`, `magick` (ImageMagick) and `potrace` are installed.
- Check any logo change at 48px as well as full size — the nav and footer use it small.
