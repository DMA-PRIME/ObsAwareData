# Changelog

## Versioning

Each release is tagged `v<version>+<data date>`, for example `v1.0.0+2026-10-16`. The two parts track different things:

- **`<version>`** ([Semantic Versioning](https://semver.org/)) identifies the rules used to build the data: file layout, columns, processing, and reliability-flag rules.
- **`<data date>`** (after `+`) is the release date of the most recent CDC source file used. Each source's own release date is listed in its changelog entry.

| Change | Example | Version |
|---|---|---|
| Incompatible structure change | Column renamed or removed, file layout changed | MAJOR (2.0.0) |
| Build rules changed, structure compatible | New flag rule or threshold method, new file or table added | MINOR (1.1.0) |
| Correction without a rule change | Documentation fix, bug fix that does not change the rules | PATCH (1.0.1) |
| Data refresh only | Same rules, newer CDC source releases | Version unchanged; only the data date changes |

Under Semantic Versioning, the part after `+` is build metadata: it does not affect version precedence. Two tags with the same version and different data dates are built with the same rules.

## 2.0.0+2026-10-23 (released 2026-10-25)

Data refresh with newer CDC source releases; the build rules are unchanged.

<!-- auto:changelog_data -->
- Source releases used, latest of each: NHSN 2026-10-23, NSSP 2026-10-21, NWSS 2026-10-23. Weeks covered: NHSN through 2026-10-17, NSSP through 2026-10-17, NWSS through 2026-10-17.
- Revision history covers 120 NHSN, 55 NSSP, 12 NWSS releases. Release assets added in this release: 51 increment (see `metadata/release_assets.csv`).
- Compared with 2.0.0+2026-10-16: 20,296 rows added and 0 removed in the latest-value tables; 191,262 values revised; 12,358 `observation_state` values changed.
<!-- /auto:changelog_data -->

## 2.0.0+2026-10-16 (released 2026-10-18)

Data refresh with newer CDC source releases; the build rules are unchanged.

<!-- auto:changelog_data -->
- Source releases used, latest of each: NHSN 2026-10-16, NSSP 2026-10-14, NWSS 2026-10-16. Weeks covered: NHSN through 2026-10-10, NSSP through 2026-10-10, NWSS through 2026-10-10.
- Revision history covers 118 NHSN, 54 NSSP, 11 NWSS releases. Release assets added in this release: 51 increment (see `metadata/release_assets.csv`).
- Compared with 2.0.0+2026-10-09: 28,509 rows added and 0 removed in the latest-value tables; 299,537 values revised; 23,901 `observation_state` values changed.
<!-- /auto:changelog_data -->

## 2.0.0+2026-10-09 (released 2026-10-14)

Changes how the latest-value tables cite their source, so that a row changes only when its value or flags change. **Incompatible change:** code that reads `extract_timestamp` from `<st>_long_latest_<year>.csv`, or uses `source_snapshot_id` or `as_of_date` there as the newest release, must be updated. Values and flags are unchanged.

- Changed: in `<st>_long_latest_<year>.csv`, `source_snapshot_id` and `as_of_date` now name the release that first published the row's current value and flags, unchanged in every later release that carries the row, instead of the newest release. The value is still the newest release's.
- Removed: `extract_timestamp` from `<st>_long_latest_<year>.csv`, which now have 15 columns. It was the same for every row of a release; the release's as-of date is in its tag. The revision history keeps it.
- Revision history: unchanged; later releases add increments as before.

Before, every row of the latest-value tables changed every week, because each carried the newest release's identifier; the repository grew by about 30-40 MB a week. Now it grows only with the rows that actually change.

<!-- auto:changelog_data -->
- Source releases used, latest of each: NHSN 2026-10-09, NSSP 2026-10-07, NWSS 2026-10-09. Weeks covered: NHSN through 2026-10-03, NSSP through 2026-10-03, NWSS through 2026-10-03.
- Revision history covers 116 NHSN, 53 NSSP, 10 NWSS releases. Release assets added in this release: none (see `metadata/release_assets.csv`).
- Compared with 1.0.0+2026-10-09: 0 rows added and 0 removed in the latest-value tables; 0 values revised; 0 `observation_state` values changed.
<!-- /auto:changelog_data -->

## 1.0.0+2026-10-09 (released 2026-10-13)

Data refresh with newer CDC source releases; the build rules are unchanged.

<!-- auto:changelog_data -->
- Source releases used, latest of each: NHSN 2026-10-09, NSSP 2026-10-07, NWSS 2026-10-09. Weeks covered: NHSN through 2026-10-03, NSSP through 2026-10-03, NWSS through 2026-10-03.
- Revision history covers 116 NHSN, 53 NSSP, 10 NWSS releases. Release assets added in this release: 51 increment (see `metadata/release_assets.csv`).
- Compared with 1.0.0+2026-10-02: 20,525 rows added and 0 removed in the latest-value tables; 223,331 values revised; 15,626 `observation_state` values changed.
<!-- /auto:changelog_data -->

## 1.0.0+2026-10-02 (released 2026-10-13)

First release: weekly COVID-19, influenza, and RSV data for the 50 states and DC from three CDC surveillance systems (NHSN hospital admissions, NSSP emergency department visits, NWSS wastewater) and US Census context, with a reliability flag on every value, the CDC source release behind every value (`metadata/source_snapshots.csv`), and every state's revision history as release assets (`metadata/release_assets.csv`). See the README for the files and METHODS.md for how they are built.

<!-- auto:changelog_data -->
- Source releases used, latest of each: NHSN 2026-10-02, NSSP 2026-09-30, NWSS 2026-10-02. Weeks covered: NHSN through 2026-09-26, NSSP through 2026-09-26, NWSS through 2026-09-26.
- Revision history covers 114 NHSN, 52 NSSP, 9 NWSS releases. Release assets added in this release: 51 full (see `metadata/release_assets.csv`).
<!-- /auto:changelog_data -->

