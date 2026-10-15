# The 21st Century Dashboard — H Heuristics

A systems dashboard for the century, built in the H Heuristics house style. Nine views, each with a headline claim, a KPI strip, sourced panels and a closing **binding term**:

| # | View | What it tracks |
|---|------|----------------|
| 01 | Overview | Headline signals, signal board, the polycrisis coupling matrix |
| 02 | Diffusion | Adoption lags, global S-curves, an interactive Bass simulator with a capital-constrained ceiling, two-margin scorecard |
| 03 | Convergence | Relative income vs the US, the China wedge, four-clocks scorecard |
| 04 | Demography | US racial/ethnic composition 2000–2060, generation gap, world population by region, TFR, median age |
| 05 | Polycrisis | Temperature + emissions, CO₂, conflict + displacement, poverty, inequality, PM₂.₅ |
| 06 | Exposure | Exposure ledger, the cooling gap, climate niche, heat-labour losses |
| 07 | Clean transition | Clean vs fossil investment, generation mix, share-sync by grid, cost curves, EV sales, energy access |
| 08 | AI & technology | Frontier training compute, AI investment, data-centre load, adoption, inference cost, three AI-transition clocks |
| 09 | Frontier | Six cost-collapse curves, R&D intensity, PCT patents, publications, notable AI models by country |
| § | Sources & method | Flags, vintage, glossary, source list per panel |

No build step. Plain HTML, CSS and JavaScript with Chart.js vendored locally; the only external request is Google Fonts (system fallbacks are declared).

## Run locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Opening `index.html` directly from disk also works.

## Deploy to GitHub Pages

1. Push to `main`.
2. Repository **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main`, Folder = `/ (root)`.
3. The site is served at `https://<user>.github.io/21st-century-dashboard/`. `.nojekyll` is included so asset paths are served as-is.

Any static host (Netlify, Cloudflare Pages, Vercel) works the same way: publish the repository root.

## Structure

```
index.html                 shell: masthead, tab nav, footer
assets/css/styles.css      design tokens (paper + midnight themes), layout
assets/js/data.js          every number on the site, with a source string per dataset
assets/js/app.js           chart factory, custom plugins, section/panel registry, routing, export
assets/vendor/chart.umd.min.js   Chart.js 4.4.7
favicon.svg
```

## Updating data

All figures live in `assets/js/data.js`. Each dataset carries a `source` string and an `approx: true` flag where values are read off published charts, interpolated or preliminary; the flag renders as `≈ approx.` on the panel footer and in the Sources view. Panels in `app.js` read from `HH_DATA` and hard-code nothing, so changing a series changes the chart, the tooltip and the CSV export together.

Scorecard thresholds (two-margin diffusion, four clocks, share-sync, AI-transition clocks) are stated in each panel's subtitle and set in `data.js` or at the top of the corresponding `render*` function in `app.js`.

## Features

- Light (paper) and dark (midnight) themes, persisted; charts re-render with the theme.
- Hash routing (`#diffusion`, `#transition`, …) so every view is linkable; ← → keys switch views.
- Per-panel **CSV** and branded **PNG** export from the panel header.
- Print stylesheet for the active view.
- Responsive down to phone widths.

## Caveats

This is an analytical instrument, not a primary data source. Values marked ≈ should be re-checked against the cited release before being quoted. The coupling matrix in the Overview is an explicit analytical judgment.

---

H Heuristics · Data · Clarity · Judgment
