# Wyoming (WY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 56
- Emergency-department regions (CDC health service areas): 13
- Wastewater sampling sites: 7 (with COVID-19 data: 7; influenza A: 5; RSV: 2)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wy_long_latest.csv` | 42,809 | 17 | 13.7 |
| `wy_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `wy_nssp_wide.csv` | 2,828 | 30 | 1.0 |
| `wy_nwss_wide.csv` | 1,120 | 24 | 0.3 |
| `wy_all_sources_wide.csv` | 316 | 461 | 1.1 |
| `wy_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 14 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 14 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 14 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 11 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 7 | 2022-07-16 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 5 | 2023-08-12 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 2 | 2023-11-18 | 2026-08-22 |

## Reliability flags

Number of rows in `wy_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 663 | 0 | 70 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 547 | 141 | 0 | 35 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,454 | 0 | 3,030 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,603 | 5,026 | 0 | 0 | 1,683 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,266 | 186 | 0 | 742 | 5,118 | 0 |
| NSSP | participation_status | 2,424 | 0 | 202 | 0 | 0 | 0 |
| NWSS | participation_status | 1,451 | 0 | 632 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,762 | 0 | 0 | 321 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,483 | 0 | 0 | 600 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WY |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 21 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 160% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.93 |
| Wastewater: same, influenza A | 0.97 |
| Wastewater: same, RSV | 0.75 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`wy_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,619,496 rows covering 42,809 distinct values. Of those, 15,881 (37.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 1,337,670 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 24,786 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wy_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `wy_nssp_wide.csv` matches the long table | PASS | 33,734 cells; missing 0, unexpected 0, differing 0 |
| `wy_nwss_wide.csv` matches the long table | PASS | 6,249 cells; missing 0, unexpected 0, differing 0 |
| `wy_all_sources_wide.csv` matches the long table | PASS | 42,809 cells; missing 0, unexpected 0, differing 0 |
| `wy_all_sources_wide.csv` census columns match `wy_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
