# MVD Analysis Suite — GitHub Pages Deployment

A single-file statistical analysis platform for the **IAEA Mutant Variety Database** (mvd.iaea.org). Nine analysis modules, dark IAEA theme, Python code panels in every module. No build step, no server — pure static HTML + PapaParse + Plotly (loaded from CDN).

## 📁 What's in this folder

```
index.html      ← the entire app (all 9 modules)
MVD_DB.csv      ← the official IAEA MVD export (≈3,510 varieties), auto-loaded on open
.nojekyll       ← tells GitHub Pages to serve files as-is (do not delete)
README.md
```

The bundled `MVD_DB.csv` is the **real IAEA Mutant Variety Database export** ("Mutant Variety Details"). The app maps its columns automatically (Common Name → Crop, Latin Name → Species, Character Improvement Details → traits, Physical/Chemical Mutagen merged, Continent → Region). Region filters use the six continents present in the data. The Trait module includes a **Development Method × Trait** view built on the database's own `MutantDevelopmentType` field (direct mutant vs. crossing) — a clean, structured stand-in for "origin/parent" analysis.

## 🚀 Deploy to GitHub Pages (5 minutes, free)

1. Create a new GitHub repository (e.g. `mvd-suite`).
2. Upload **all four files** from this folder to the repo root (drag them into the GitHub web uploader, or `git push`).
3. In the repo: **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Branch: **main**, folder: **/ (root)** → **Save**.
6. Wait ~1 minute. Your site is live at:
   `https://<your-username>.github.io/<repo-name>/`

That's it. Opening the page auto-loads `MVD_DB.csv` from the same folder — no CORS problem, because the file is served from the same origin as the app.

## 🔄 Using the real / latest MVD data

The bundled `MVD_DB.csv` is a small **sample** so the app works out of the box. To use the real database:

**Option A — bundle the official export (recommended)**
1. Go to **mvd.iaea.org → Search Varieties**, leave filters empty, **Search**, then **Download / Export CSV**.
2. Rename it to `MVD_DB.csv` and replace the file in your repo (keep the exact column headers).
3. Commit. The site now auto-loads the full database for everyone.

**Option B — each user loads their own**
- **📁 Load Local CSV** or drag-and-drop a CSV they downloaded themselves.

**Option C — fetch live (best-effort)**
- **⚡ Fetch Latest (mvd.iaea.org)** tries public CORS proxies (allorigins → corsproxy.io → cors.sh). These are third-party and sometimes rate-limited; if they fail, fall back to A or B.

The app also normalises common header variants and derives `Region`, `Mutagen_Category` (Physical/Chemical), `Crop_Group`, and `Decade` automatically.

## 📊 The 9 modules

1. 🌿 **Crop Explorer** — one species, one-page dashboard (timeline, countries, mutagens, traits, explants, institutions, Explant × Trait).
2. 📊 **Dataset Overview** — frequency tables/charts for any column; programme strength.
3. 📅 **Temporal Analysis** — annual/decadal trends, cumulative growth, Mann-Kendall + Sen's slope.
4. 🌍 **Cross-Table & Compare** — heatmap / stacked % / grouped bar / sunburst for any two variables.
5. 🧬 **Mutagen Analysis** — Physical vs Chemical, decadal shift, Crop/Country × Mutagen, dose histogram.
6. 🏷️ **Trait Analysis** — top traits, 7-category split, Crop × Trait, decade shift, region comparison.
7. 🧫 **Explant × Trait** — tissue → outcome: count + row-normalised % heatmaps and a Chi-Square test.
8. 📈 **Advanced Statistics** — Chi-Square, detailed Mann-Kendall, descriptive stats + histogram + box plot.
9. 💾 **Export & Report** — processed CSV, plain-text summary report, PNG/SVG for every chart.

## 🔍 Botanical search

In any crop/species field, type a common **or** Latin name — e.g. `lens` finds *Lens culinaris* (Lentil). Searches both `Crop` and `Species` columns and tolerates small typos (Levenshtein ≤ 2).

## 🐍 Python panels

Every analytical module has a collapsible panel showing the equivalent **pandas / matplotlib / seaborn / scipy** code, with short notes on what each library does — for transparency and as a teaching aid.

---

Data: IAEA Mutant Variety Database — https://mvd.iaea.org
