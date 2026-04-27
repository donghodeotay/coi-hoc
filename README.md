# Coi Học — Site

Static site for Mika's Grade-9 learning platform. Designed for **GitHub Pages**, no backend required.

## Structure

```
site/
├── index.html              ← main hub Mika opens
├── parent/
│   └── index.html          ← parent dashboard (Coach Console lite)
├── lessons/
│   ├── toan9/
│   │   └── index.html      ← (drop the toan9 lesson HTML here)
│   ├── lichsu9/
│   ├── diali9/
│   ├── vatly9/
│   ├── hoahoc9/
│   ├── sinhhoc9/
│   ├── nguvan9/
│   └── gdcd9/
└── README.md
```

## Filling in the lesson folders

Each subject's lesson HTML currently lives as a Cowork artifact:

| Subject | Artifact ID | Goes to |
|---|---|---|
| Toán | `toan9-hanh-trinh-chinh-phuc` | `lessons/toan9/index.html` |
| Lịch sử | `lichsu9-hanh-trinh-chinh-phuc` | `lessons/lichsu9/index.html` |
| Địa lí | `diali9-hanh-trinh-chinh-phuc` | `lessons/diali9/index.html` |
| Vật lý | `vatly9-hanh-trinh-chinh-phuc` | `lessons/vatly9/index.html` |
| Hoá học | `hoahoc9-hanh-trinh-chinh-phuc` | `lessons/hoahoc9/index.html` |
| Sinh học | `sinhhoc9-hanh-trinh-chinh-phuc` | `lessons/sinhhoc9/index.html` |
| Ngữ văn | `nguvan9-hanh-trinh-chinh-phuc` | `lessons/nguvan9/index.html` |
| GDCD | `gdcd9-hanh-trinh-chinh-phuc` | `lessons/gdcd9/index.html` |

Two ways to copy them in:

1. **From Cowork sidebar**: open the artifact, use the download/export option, save as `index.html` in the matching folder.
2. **Ask me to write them directly**: each lesson is ~80–100 KB of self-contained HTML. I can drop them all in one batch.

## Deploying to GitHub Pages

1. Initialise the repo (one-time):
   ```bash
   cd "Learning brainStorm/site"
   git init
   git add .
   git commit -m "Initial Coi Học site scaffold"
   ```

2. Create a public GitHub repo (e.g. `coi-hoc`), then:
   ```bash
   git remote add origin https://github.com/<your-user>/coi-hoc.git
   git branch -M main
   git push -u origin main
   ```

3. In the repo on GitHub: **Settings → Pages → Source: deploy from `main`, folder `/` (root)** → Save.

4. After ~1 minute the site is live at `https://<your-user>.github.io/coi-hoc/`.

5. Mika opens that URL on her phone or laptop. Progress is stored in browser localStorage on her device.

## How localStorage / progress works

Each lesson saves to its own key:

- `toan9-progress`, `lichsu9-progress`, `diali9-progress`, `vatly9-progress`, `hoahoc9-progress`, `sinhhoc9-progress`, `nguvan9-progress`, `gdcd9-progress`

A shared key tracks the cross-subject streak:

- `toan9-activity` (do **not** rename — the name is historic, all subjects write to it)

The hub `index.html` and the parent dashboard read these keys to show progress and streaks. Same domain ⇒ all keys visible to all pages.

**Caveat**: progress lives on the device that did the work. Clearing the browser, or moving to a different device, resets it. Phase 5/6 of the master plan adds an optional sync backend.

## Design constraints baked into every page

- **Mobile-responsive** at 375 px (target: Mika's phone)
- **Self-contained** — no external CSS or JS, no analytics, no trackers
- **Light mode** via `:root { color-scheme: light }`
- **localStorage keys in one config object** at top of each lesson — so a future sync layer can swap them without rewriting every page
- **No Cowork-specific APIs** in lesson files (those only exist in the Cowork-side Coach Console)

## Updating

When a new lesson ships:

1. Drop the new HTML into the right `lessons/<subject>/` folder
2. Update the SUBJECTS list at the bottom of `index.html` if the lesson name changed
3. Commit + push — GitHub Pages auto-deploys

That's it.
