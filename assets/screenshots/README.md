# Screenshots

This directory holds the screenshots referenced by `index.md` (the landing page at <https://jziesing.github.io/ai-agent-usage-downloads/>).

**These are published as-is by `scripts/publish_release.sh`** — it mirrors this folder into the public repo on each release. Drop real PNGs in here (with the exact filenames below) **before** running the publish script, or the live landing page will show broken image icons until they exist.

## Expected filenames

The landing page references these files by exact name. Use the same filename and they'll appear automatically on the next publish.

| File | What it should show |
| --- | --- |
| `01-usage-overview.png` | Home → Usage tab. Per-provider cost and token rollups (the cost-tracking baseline). |
| `02-insights-grid.png` | Output tab → Insights grid, zoomed out so the spread of individual + manager cards is visible at once. |
| `03-repeat-prompts-card.png` | Repeat Prompts card expanded into its modal, showing clustered prompts and session drilldown. |
| `04-tasks-you-could-learn.png` | Tasks You Could Learn card after the on-device LLM has produced its summary. |
| `05-search-tab.png` | Search tab with a full-text query entered, a result snippet visible, and a session selected. |
| `06-settings-transcripts.png` | Settings → Transcripts section showing storage stats, the capture toggle, purge, and compact controls. |

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
