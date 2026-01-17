# GRT-Chrono-Import-Tool
Simple standalone HTML to import Garmin/Athlon Chrono data into GRT.

## Live link

GitHub Pages:

- https://mrimp.github.io/GRT-Chrono-Import-Tool/

Direct tool file (bypasses the landing page):

- https://mrimp.github.io/GRT-Chrono-Import-Tool/GRT%20Chrono%20Importer.html

> If the GitHub Pages link 404s, enable it in **Repo → Settings → Pages** (Deploy from branch: `main`, folder: `/root`).
>
New: Export Diagnostics ZIP

We added a one-click export to help debug weird imports (units, parsing, missing shots, etc.).

How to use it

Open the Importer HTML in your browser.
Import your file(s) like normal (CSV/XLS/XLSX — Garmin/Athlon/etc.).
After the import finishes, click Export Diagnostics ZIP.
Your browser will download a ZIP containing:
diagnostics.json
Import details per file (detected device/type, units, column mapping, start row, plus summary stats like count/mean/SD/ES/min/max).
raw_rows/*.csv (one CSV per imported file/session)
The raw parsed rows the importer used (shot #, velocity, PF/time/note if present, and the original “velocityRaw” cell text).

When to use it

Use this button anytime:
The units look wrong (m/s vs fps conversion issues),
The shot count doesn’t match what the device shows,
You see wild SD/ES or obvious outliers that shouldn’t be there,
A Sessions workbook imports strangely.
What to send back
Please attach the ZIP in your feedback along with:
what device exported the file (Garmin/Athlon/etc.),
what units the device/app was set to,
what you expected vs what the importer showed.

## Offline usage

Download the HTML and open it in a browser:

- https://raw.githubusercontent.com/mrimp/GRT-Chrono-Import-Tool/main/GRT%20Chrono%20Importer.html

<img width="2415" height="3755" alt="_C__Users_bill_Downloads_GRT_Importer_Standard_v080_release_FINAL html" src="https://github.com/user-attachments/assets/4169ca63-375a-4542-8ca1-26ed96fe4230" />


## GRT Importer Standard v0.80.5.5 (RELEASE)

### Highlights
- Robust import for **Athlon RangeCraft** (`.xlsx`) + **Garmin** (`.csv`) with better real-world tolerance
- Fully **single-file**, **offline**, and **GitHub Pages-safe** (no `_files` folder, no external CSS/JS deps)

### Smarter parsing (multi-language + messy exports)
- Language-agnostic header detection (handles translated/edited headers)
- Quote-aware CSV parsing (supports **Notes fields with commas**)
- International number parsing (`1,234.56` and `1.234,56`)
- Improved delimiter detection (comma / semicolon / tab)

### Units: fixed + hardened
- Per-file unit detection (Garmin/Athlon can differ in the same batch)
- Correct Metric/Imperial display conversion (prevents “fps shown as m/s”)
- Export/import to GRT stays **m/s internally** for consistency

### Column Mapping (failsafe)
- Mapping modal appears when detection confidence is low
- Optional **remember mapping** per format on this browser/device
- Mapping auto-invalidates if it yields 0 valid shots, then re-prompts

### Notes column support (new)
- Optional **Notes / Shot Notes / Comment** column auto-detect + manual mapping
- Notes carried through into exported data (per-shot note field)

### UI/UX + release hardening
- Removed remaining “Tailwind-ish” runtime class dependencies (Incognito-safe)
- Toast + sparkline coloring now relies on internal CSS only
- Filename truncation/ellipsis so long names don’t push pills out of cards
- Restored status pill colors + metric score coloring (Tight/OK/Wide)

### Bug fixes
- Fixed `sdDisp is not defined`
- Fixed `grid is not defined`
- Fixed “files load but no cards appear” (renderer helpers restored)
- Fixed hidden/show toggles after CSS refactor

### Download
- `GRT_Importer_Standard_v0.80.6.6_RELEASE_NO_TAILWINDISH_CLEAN.html`



