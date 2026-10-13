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

## 1.0.0+2026-10-02 (released 2026-10-13)

First release: weekly COVID-19, influenza, and RSV data for the 50 states and DC from three CDC surveillance systems (NHSN hospital admissions, NSSP emergency department visits, NWSS wastewater) and US Census context, with a reliability flag on every value, the CDC source release behind every value (`metadata/source_snapshots.csv`), and every state's revision history as release assets (`metadata/release_assets.csv`). See the README for the files and METHODS.md for how they are built.

<!-- auto:changelog_data -->
- Source releases used, latest of each: NHSN 2026-10-02, NSSP 2026-09-30, NWSS 2026-10-02. Weeks covered: NHSN through 2026-09-26, NSSP through 2026-09-26, NWSS through 2026-09-26.
- Revision history covers 114 NHSN, 52 NSSP, 9 NWSS releases. Release assets added in this release: 51 full (see `metadata/release_assets.csv`).
<!-- /auto:changelog_data -->

