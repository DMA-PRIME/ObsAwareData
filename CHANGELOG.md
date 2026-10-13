# Changelog

## Versioning

Each release is tagged `v<version>+<data date>`, for example `v1.0.0+2026-08-28`. The two parts track different things:

- **`<version>`** ([Semantic Versioning](https://semver.org/)) identifies the rules used to build the data: file layout, columns, processing, and reliability-flag rules.
- **`<data date>`** (after `+`) is the release date of the most recent CDC source file used. Each source's own release date is listed in its changelog entry.

| Change | Example | Version |
|---|---|---|
| Incompatible structure change | Column renamed or removed, file layout changed | MAJOR (2.0.0) |
| Build rules changed, structure compatible | New flag rule or threshold method, new file or table added | MINOR (1.1.0) |
| Correction without a rule change | Documentation fix, bug fix that does not change the rules | PATCH (1.0.1) |
| Data refresh only | Same rules, newer CDC source releases | Version unchanged; only the data date changes |

Under Semantic Versioning, the part after `+` is build metadata: it does not affect version precedence. Two tags with the same version and different data dates are built with the same rules.

## 1.2.0+2026-10-09 (released 2026-10-13)

Data refresh with newer CDC source releases, and changes to how the data are dated and distributed. File layout and columns are unchanged except as noted.

- Changed: `extract_timestamp` is now a date. In `<st>_long_latest.csv` it is this release's as-of date (only CDC source files released on or before it were used), the same for every row. In the revision history it is the as-of date of the release that first published the row's source release, so a published row never changes. It used to be the time the dataset was built, which changed every row on every rebuild even when no value changed.
- Changed: the revision history is distributed as one full file per state (`<st>_long_all_versions.csv.gz`) followed by one small file per later release with only the newly published source releases (`<st>_long_all_versions_added_<as-of date>.csv.gz`). `metadata/release_assets.csv` lists every file of every state in order and has new columns `tag`, `version`, `kind`, `as_of`, `snapshots`, and `rows`. This release carries a new full file for every state.
- Changed: South Carolina's revision history is no longer kept in `data/SC/`; download it from the releases like every other state. `revision_history_location` in `metadata/coverage_summary.csv` is now `release` for every state.
- Sources: every CDC release used is kept unmodified in a public [archive of CDC releases](https://github.com/jiandewu/ObsAwareData-pipeline). Releases from 2026-10-07 on are the API's CSV export, which rounds the few NHSN values that end in .5 half to even, where the earlier files rounded them half up; such values can differ by 1 between releases before and after that date.
- Removed: 803 rows of NWSS `participation_status` for 5 wastewater sites in Michigan (`ID:900`, 187 rows) and Oklahoma (`ID:1696`, `ID:1704`, `ID:1708`, `ID:1709`, 616 rows). Site `ID:900` is absent from the newest NWSS releases, and the four Oklahoma sites have fewer weeks in them; this field is computed from the newest release. Their wastewater activity values are kept.
- Iowa: in the newest NSSP releases, Iowa's ED values after the week ending 2026-06-27 are blank (previously reported through 2026-08-08), so its ED series now ends earlier.
- Revised values: in the states checked (Iowa, Michigan, Oklahoma), most come from CDC's NSSP releases (smoothed ED percentages and trend labels) and from revised NWSS activity levels.

<!-- auto:changelog_data -->
- Source releases used, latest of each: NHSN 2026-10-09, NSSP 2026-10-07, NWSS 2026-10-09. Weeks covered: NHSN through 2026-10-03, NSSP through 2026-10-03, NWSS through 2026-10-03.
- Revision history covers 116 NHSN, 53 NSSP, 10 NWSS releases. Release assets added in this release: 51 full (see `metadata/release_assets.csv`).
- Compared with 1.1.0+2026-08-28: 154,587 rows added and 803 removed in the latest-value tables; 350,932 values revised; 84,555 `observation_state` values changed.
<!-- /auto:changelog_data -->

## 1.1.0+2026-08-28 (released 2026-09-30)

Adds the full revision history for every state. Same source data as 1.0.0+2026-08-28.

- New: `<st>_long_all_versions.csv.gz` for all 50 states and DC (about 840 MB in total), distributed as GitHub Release assets rather than in the repository. South Carolina's copy stays in `data/SC/`.
- New: `metadata/release_assets.csv` with each asset's download link, size, and SHA-256.
- New column in `metadata/coverage_summary.csv`: `revision_history_location` (`repo` or `release`); `revision_history_included` is now true for every state.
- Quality reports: every state now includes a revision-history summary and the two revision-history consistency checks.
- No change to any existing data table (CSV or the SC revision-history file).

## 1.0.0+2026-08-28 (released 2026-09-30)

First public release.

- 50 states and DC: latest-value long table, NHSN/NSSP/NWSS wide tables, all-sources wide table, state Census context, and a per-state quality report.
- South Carolina: full revision history across 100 NHSN, 45 NSSP, and 4 NWSS releases (`sc_long_all_versions.csv.gz`).
- Source releases used, latest of each: NHSN 2026-08-14, NSSP 2026-08-14, NWSS 2026-08-28. Weeks covered: NHSN and NSSP through 2026-08-08, NWSS through 2026-08-22.
