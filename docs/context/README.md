# delphi-archive — context map

Last updated: 2026-11-12 @ a1c30fa

## TL;DR
- Git-versioned **content archive** of research PDFs. No code, build, tests or runtime.
- `stock_reports/<TICKER>/report_<TICKER>_<YYYYMMDD_HHMMSS_micro>.pdf` — ~765 ticker folders.
- `studies/<domain>/<study_slug>/…pdf` — ~140 PDFs across 13 domains.
- **Written only by `cerberus_workbench`**: `task sync` (= `sync:git`) runs `scripts/sync_delphi_archive.py --destination ../delphi-archive` there. `sync:preview` = dry run. Fix bad output in workbench and re-sync, never by hand.
- Commits are data drops (`chore: data update`).

## Requirements / invariants
- Append-mostly by hand: don't delete, rename or overwrite reports/studies manually unless explicitly asked. Note the workbench sync itself replaces each folder's PDF with the latest (older PDFs deleted; history only in git).
- Keep the report naming convention; never regenerate or renumber historical reports.
- New studies go under an existing domain; new domain only when none fits.
- Update `README.md` contents table when a study or report category is added.

## Features
| Feature | Status | Notes |
|---|---|---|
| Per-ticker stock reports | done | produced by workbench stock-report pipeline |
| Domain-organized study PDFs | done | produced by workbench `src/studies` |
| Contents index | stale | `README.md` table lacks `liquidity/`, `stats/`, `technical-reports/` |

## Architecture
Pure sink. Flow: `cerberus_workbench/outputs/{stock_reports,studies}` → `scripts/sync_delphi_archive.py` (copies latest PDFs) → this repo → manual `git commit`. Same script can target a Box folder (`task sync:box`, `CERBERUS_BOX_DIR`). No other project reads or writes here.

## Glossary
| Term | Meaning |
|---|---|
| Stock report | Per-ticker equity research PDF from workbench |
| Study | Quant research PDF (one folder per study slug) from workbench studies framework |
| Domain | Top-level folder under `studies/` |

## Gotchas
- Large binary repo: avoid `git add -A` sweeps outside a sync; never rewrite history.
- Study domains on disk (13) differ from `AGENTS.md` list (10): `liquidity`, `stats`, `technical-reports` are also in use.

## Index
| File | Open when |
|---|---|
| [structure.md](structure.md) | locating content / filing a new study |
| [decisions.md](decisions.md) | why it's a separate repo; open gaps |
