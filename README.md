# MVD Analysis Suite v4 — GitHub Pages Deployment

A single-file statistical analysis platform for the **IAEA Mutant Variety Database** (mvd.iaea.org). Nine analysis modules, dark IAEA theme, Python code panels in every module, **English / Turkish interface**, and a phone-friendly layout. No build step, no server — pure static HTML + PapaParse + Plotly + JSZip (loaded from CDN).

Live: https://ozancet.github.io/mvd/

## 📁 What's in this folder

```
index.html      ← the entire app (all 9 modules, EN/TR)
MVD_DB.csv      ← the official IAEA MVD export (3,511 varieties), auto-loaded on open
.nojekyll       ← tells GitHub Pages to serve files as-is (do not delete)
README.md
```

The bundled `MVD_DB.csv` is the **real IAEA Mutant Variety Database export** ("Mutant Variety Details"). The app maps its columns automatically (Common Name → Crop, Latin Name → Species, Character Improvement Details → traits, Physical/Chemical Mutagen merged, Continent → Region) and derives `Region`, `Mutagen_Category`, `Crop_Group` and `Decade`.

## 🌐 Language (EN / TR)

The **EN | TR** switch sits at the top right of every page. The choice is remembered in the browser.

- Share a Turkish link directly: `https://ozancet.github.io/mvd/?lang=tr`
- The default is English, so a presentation link opens in English regardless of the browser language.
- Interface text, result sentences, chart titles/axes/categories, alerts, the summary report and the ZIP README are translated.
- **Data values are never translated** — crop, country, variety and institution names, and free-text trait descriptions appear exactly as recorded by the IAEA, so filters and exports are identical in both languages.
- Python code panels stay in English (they are code).

## 🧩 Text enrichment (regex, deterministic)

Some useful information is written inside the free-text fields rather than in its own column. On load, the app reads it with fixed text patterns (regular expressions) — no AI, no guessing:

| Field | Raw export | After enrichment |
|---|---|---|
| Mutagen dose (Gy) | 0% (no column) | ≈50% |
| Mutagen type | 81% | 87% |

- Dose is read from the mutagen fields, the short description and the miscellaneous notes, **radiation units only** (Gy, kGy, krad). Millimetre/millimolar values are deliberately excluded because "mm" is also used for plant and grain measurements.
- Every enriched value is a literal match you can find in the record's text. The parent cultivar is **not** extracted (too varied to parse reliably) — use the website for it.

## 🚀 Deploy to GitHub Pages

1. Upload **all four files** to the repo root.
2. **Settings → Pages → Deploy from a branch → main / (root) → Save.**
3. After ~1 minute the site is live at `https://<username>.github.io/<repo>/`.

To refresh the data: download a new export from **mvd.iaea.org → Search Varieties → Download / Export CSV**, rename it to `MVD_DB.csv`, replace the file in the repo and commit. Users can also load their own file with **📁 Load Local CSV** or drag-and-drop.

## 📊 The 9 modules

1. 🌿 **Crop Explorer** — one species, one-page dashboard (timeline, countries, mutagens, traits, explants, institutions, Explant × Trait).
2. 📊 **Dataset Overview** — frequency tables/charts for any column; programme strength.
3. 📅 **Temporal Analysis** — annual/decadal trends, cumulative growth, Mann-Kendall + Sen's slope with a plain-language verdict.
4. 🌍 **Cross-Table & Compare** — heatmap / stacked % / grouped bar / bubble grid for any two variables.
5. 🧬 **Mutagen Analysis** — Physical vs Chemical, decadal shift, Crop/Country × Mutagen, dose histogram.
6. 🏷️ **Trait Analysis** — top traits, 11 categories with a Crop Group filter, Crop × Trait, decade shift, Development × Trait.
7. 🧫 **Explant × Trait** — tissue → outcome: count + row-normalised % heatmaps and a Chi-Square test, with a coverage note.
8. 📈 **Advanced Statistics** — Descriptive Statistics first (plain-language dose/year summary + histogram), then Chi-Square and detailed Mann-Kendall.
9. 💾 **Export & Report** — one-click ZIP (processed CSV + summary report + every chart), PNG/SVG per chart.

## 🔍 Botanical search

In any crop/species field, type a common **or** Latin name — e.g. `lens` finds *Lens culinaris* (Lentil). Searches both `Crop` and `Species` columns and tolerates small typos.

## 🐍 Python panels

Every analytical module has a collapsible panel showing the equivalent **pandas / matplotlib / seaborn / scipy** code, with short notes on what each library does.

---

Data: IAEA Mutant Variety Database — https://mvd.iaea.org
