# PressAtlas — World News Map

Interactive world map linking every country to its leading free newspaper, with GDELT-powered global topic search and a coverage thread builder.

**100% free · no API keys · no backend · no tracking · no AI services**

---

## What it does

| Feature | How it works |
|---|---|
| **Click any country** | Opens its leading free newspaper in a side panel, with local clock and Google Translate link for non-English papers |
| **Topic search → heatmap** | Queries GDELT Doc 2.0 API; countries glow by article count |
| **☉ Coverage Thread** | Pulls up to 250 articles, groups by country, shows top headlines with direct links + opens that country's newspaper |
| **Country picker** | Dropdown to jump to any of ~170 countries/territories |
| **Zoom / pan** | D3 zoom, +/− buttons, reset |

---

## Data sources

| Source | What it provides | Licence |
|---|---|---|
| [GDELT Project](https://www.gdeltproject.org) | Article search, country attribution | Open / free |
| [TopoJSON world-110m](https://github.com/topojson/world-atlas) | Country geometry (inlined) | BSD-3 |
| [D3.js](https://d3js.org) | Map projection and interaction | ISC |
| [Natural Earth](https://www.naturalearthdata.com) | Underlying geodata | Public domain |
| Newspaper list | Hand-curated ~170 countries | MIT (this repo) |

No data leaves your browser except for the GDELT query (which is public by nature) and the Google Fonts load.

---

## Hosting on GitHub Pages

```bash
git init
git remote add origin https://github.com/<you>/pressatlas.git
git add index.html README.md _config.yml
git commit -m "init"
git push -u origin main
```

Then in the repo → **Settings → Pages → Source: Deploy from branch → main / (root)**.

Live at `https://<you>.github.io/pressatlas` in ~60 seconds. No build step, no dependencies to install.

---

## Local development

```bash
# Any static server works — Python example:
python3 -m http.server 8080
# open http://localhost:8080
```

Do not open `index.html` as a `file://` URL — GDELT fetch will be blocked by browser CORS policy.

---

## Rate limiting

GDELT's free API throttles by IP. The app enforces:
- Minimum **6 seconds** between requests (self-imposed)
- **30 second cool-down** after receiving HTTP 429

If you see a rate-limit error, wait and retry.

---

## Adding / editing newspapers

All newspaper data is in the `const PAPERS = { ... }` object inside `index.html`. Each entry:

```js
"356": { c:"India", n:"The Times of India", u:"https://timesofindia.indiatimes.com",
         d:"World's largest-circulation English daily; fully free online.", code:"IN", lang:"en" }
```

Key = ISO 3166-1 numeric country code. `lang:"en"` suppresses the Google Translate button.

---

## Tech stack

- **D3.js v7** — map, zoom, projection
- **TopoJSON v3** — topology decoding
- **GDELT Doc 2.0 API** — article search (free, CORS-enabled)
- **Google Fonts** — Fraunces + Spline Sans Mono
- Zero build tooling — single self-contained `index.html`

---

## Licence

MIT — see [LICENSE](LICENSE)
