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

<!-- Describe what changed in the build rules for this version. -->

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
