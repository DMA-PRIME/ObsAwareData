# Oregon (OR): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 41
- Emergency-department regions (CDC health service areas): 14
- Wastewater sampling sites: 38 (with COVID-19 data: 38; influenza A: 38; RSV: 37)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (86 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (11 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `or_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `or_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `or_long_latest_2022.csv` | 12,661 | 15 | 2.8 |
| `or_long_latest_2023.csv` | 19,469 | 15 | 4.4 |
| `or_long_latest_2024.csv` | 22,541 | 15 | 5.1 |
| `or_long_latest_2025.csv` | 23,861 | 15 | 5.4 |
| `or_long_latest_2026.csv` | 17,928 | 15 | 4.0 |
| `or_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `or_nssp_wide.csv` | 3,180 | 30 | 1.2 |
| `or_nwss_wide.csv` | 7,482 | 24 | 2.0 |
| `or_all_sources_wide.csv` | 324 | 1,079 | 2.6 |
| `or_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 15 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 15 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 15 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 15 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 38 | 2022-01-01 | 2026-10-10 |
| Wastewater (NWSS) | influenza | 38 | 2022-01-01 | 2026-10-10 |
| Wastewater (NWSS) | rsv | 37 | 2022-09-03 | 2026-10-10 |

## Reliability flags

Number of rows in `or_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 690 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 628 | 68 | 0 | 48 | 19 | 209 |
| NHSN | hospital_reporting_count | 744 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 8,885 | 0 | 655 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 8,224 | 2,891 | 0 | 0 | 1,605 | 0 |
| NSSP | ed_visit_percent_smoothed | 8,689 | 499 | 0 | 1,079 | 2,453 | 0 |
| NSSP | participation_status | 2,332 | 0 | 636 | 0 | 0 | 0 |
| NWSS | participation_status | 16,484 | 0 | 2,267 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 17,464 | 0 | 0 | 1,287 | 0 | 0 |
| NWSS | wastewater_activity_level | 17,464 | 0 | 0 | 1,287 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for OR |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 37 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 38% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.76 |
| Wastewater: same, influenza A | 0.66 |
| Wastewater: same, RSV | 0.58 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`or_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,781,155 rows covering 97,117 distinct values. Of those, 36,946 (38.0%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 1,805,573 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 661,032 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `or_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `or_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `or_nssp_wide.csv` matches the long table | PASS | 37,948 cells; missing 0, unexpected 0, differing 0 |
| `or_nwss_wide.csv` matches the long table | PASS | 56,253 cells; missing 0, unexpected 0, differing 0 |
| `or_all_sources_wide.csv` matches the long table | PASS | 97,117 cells; missing 0, unexpected 0, differing 0 |
| `or_all_sources_wide.csv` census columns match `or_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
