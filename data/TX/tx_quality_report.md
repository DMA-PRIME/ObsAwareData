# Texas (TX): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 48
- Emergency-department regions (CDC health service areas): 61
- Wastewater sampling sites: 123 (with COVID-19 data: 123; influenza A: 80; RSV: 80)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `tx_long_latest.csv` | 233,465 | 17 | 79.4 |
| `tx_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `tx_nssp_wide.csv` | 12,524 | 30 | 5.0 |
| `tx_nwss_wide.csv` | 13,298 | 24 | 3.0 |
| `tx_all_sources_wide.csv` | 316 | 3,227 | 6.4 |
| `tx_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 57 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 57 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 57 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 57 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 123 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 80 | 2022-03-05 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 80 | 2022-03-05 | 2026-08-22 |

## Reliability flags

Number of rows in `tx_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 661 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 665 | 14 | 0 | 44 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 31,437 | 0 | 6,135 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 32,810 | 7,717 | 0 | 0 | 9,569 | 0 |
| NSSP | ed_visit_percent_smoothed | 33,677 | 612 | 0 | 4,420 | 11,387 | 0 |
| NSSP | participation_status | 4,040 | 0 | 8,282 | 0 | 0 | 0 |
| NWSS | participation_status | 25,213 | 0 | 1,638 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 25,527 | 0 | 0 | 1,324 | 0 | 0 |
| NWSS | wastewater_activity_level | 20,508 | 10 | 0 | 6,333 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for TX |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 119 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 63% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.57 |
| Wastewater: same, influenza A | 0.25 |
| Wastewater: same, RSV | 0.25 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`tx_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 6,525,600 rows covering 233,465 distinct values. Of those, 72,285 (31.0%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 5,951,430 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 317,130 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `tx_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `tx_nssp_wide.csv` matches the long table | PASS | 150,086 cells; missing 0, unexpected 0, differing 0 |
| `tx_nwss_wide.csv` matches the long table | PASS | 80,553 cells; missing 0, unexpected 0, differing 0 |
| `tx_all_sources_wide.csv` matches the long table | PASS | 233,465 cells; missing 0, unexpected 0, differing 0 |
| `tx_all_sources_wide.csv` census columns match `tx_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
