# Nebraska (NE): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 31
- Emergency-department regions (CDC health service areas): 25
- Wastewater sampling sites: 21 (with COVID-19 data: 21; influenza A: 18; RSV: 18)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ne_long_latest.csv` | 91,511 | 17 | 30.6 |
| `ne_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ne_nssp_wide.csv` | 5,252 | 30 | 2.1 |
| `ne_nwss_wide.csv` | 3,678 | 24 | 0.9 |
| `ne_all_sources_wide.csv` | 316 | 1,007 | 2.5 |
| `ne_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-09-26 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 23 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 23 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 23 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 23 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 21 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 18 | 2023-08-05 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 18 | 2023-08-05 | 2026-08-22 |

## Reliability flags

Number of rows in `ne_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 605 | 81 | 0 | 38 | 9 | 209 |
| NHSN | hospital_reporting_count | 724 | 9 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 7,074 | 0 | 8,682 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 7,038 | 9,315 | 0 | 0 | 4,655 | 0 |
| NSSP | ed_visit_percent_smoothed | 7,425 | 377 | 0 | 1,069 | 12,137 | 0 |
| NSSP | participation_status | 1,212 | 0 | 3,838 | 0 | 0 | 0 |
| NWSS | participation_status | 7,193 | 0 | 1,428 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 7,653 | 0 | 0 | 968 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,261 | 0 | 0 | 2,360 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NE |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 77 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 107% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.96 |
| Wastewater: same, RSV | 0.94 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ne_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,850,375 rows covering 91,511 distinct values. Of those, 16,247 (17.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 2,491,110 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 102,225 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ne_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ne_nssp_wide.csv` matches the long table | PASS | 62,822 cells; missing 0, unexpected 0, differing 0 |
| `ne_nwss_wide.csv` matches the long table | PASS | 25,863 cells; missing 0, unexpected 0, differing 0 |
| `ne_all_sources_wide.csv` matches the long table | PASS | 91,511 cells; missing 0, unexpected 0, differing 0 |
| `ne_all_sources_wide.csv` census columns match `ne_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
