# Screenshots

This directory holds the screenshots referenced by `index.md` (the landing page at <https://jziesing.github.io/ai-agent-usage-downloads/>).

**These are published as-is by `scripts/publish_release.sh`** — it mirrors this folder into the public repo on each release. Drop real PNGs in here (with the exact filenames below) **before** running the publish script, or the live landing page will show broken image icons until they exist.

## Expected filenames

The landing page references these files by exact name. Use the same filename and they'll appear automatically on the next publish.

| File | What it should show |
| --- | --- |
| `hero.png` | The hero graphic — a magnifying lens over a neural network, ringed by token categories. |
| `01-home.png` | Home — KPI cards, spend-over-time chart, and provider/date filters. |
| `02-insights.png` | Insights grid — individual + manager cards (cost, patterns, git attribution). |
| `03-dashboards.png` | Dashboards — a saved dashboard scoped by project + date with a custom card selection. |
| `04-output.png` | Output — session list with git-linked commits and confidence bands. |
| `05-forecast.png` | Forecast — spend projections with confidence bands over 1w / 1m / 3m / 1y. |
| `06-setup.png` | Setup — data sources, GitHub token, and git folder configuration. |

## Recommended dimensions

- **Preferred:** 2880×1800 PNG (matches the App Store screenshot dimensions; sharp on Retina).
- **Acceptable:** any 16:10 PNG or WebP at 1440×900 or larger. WebP is fine and produces smaller files.
- **Keep under ~500 KB each** if possible so the landing page stays fast. `pngquant` or `cwebp -q 80` work well.

## How to replace

1. Capture the screenshot in the app (Cmd+Shift+4, then Space to grab the window).
2. Crop/resize to one of the dimensions above.
3. Save it into this directory using the exact filename from the table.
4. Re-run `scripts/publish_release.sh` (or commit + push the public repo). GitHub Pages rebuilds automatically — no local Jekyll build needed.

## Adding new screenshots

GitHub Pages publishes every file in this folder, so an unreferenced image is still reachable at its URL — it just won't appear to readers until a page links to it. To surface a brand-new screenshot, add an `![alt text](assets/screenshots/your-file.png)` line to `index.md` in the same change.
