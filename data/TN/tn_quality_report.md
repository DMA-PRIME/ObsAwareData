# Tennessee (TN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 47
- Emergency-department regions (CDC health service areas): 28
- Wastewater sampling sites: 10 (with COVID-19 data: 10; influenza A: 4; RSV: 4)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (105 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `tn_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `tn_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `tn_long_latest_2022.csv` | 5,995 | 15 | 1.4 |
| `tn_long_latest_2023.csv` | 20,063 | 15 | 4.9 |
| `tn_long_latest_2024.csv` | 20,147 | 15 | 4.9 |
| `tn_long_latest_2025.csv` | 19,439 | 15 | 4.8 |
| `tn_long_latest_2026.csv` | 15,708 | 15 | 3.9 |
| `tn_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `tn_nssp_wide.csv` | 6,148 | 30 | 2.4 |
| `tn_nwss_wide.csv` | 1,032 | 24 | 0.2 |
| `tn_all_sources_wide.csv` | 324 | 845 | 2.1 |
| `tn_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-28 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 29 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 29 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 29 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 29 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 10 | 2022-01-01 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 4 | 2023-06-17 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 4 | 2023-06-17 | 2026-10-17 |

## Reliability flags

Number of rows in `tn_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 687 | 0 | 76 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 694 | 6 | 0 | 46 | 17 | 209 |
| NHSN | hospital_reporting_count | 746 | 17 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 17,796 | 0 | 648 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 17,318 | 4,171 | 0 | 0 | 3,103 | 0 |
| NSSP | ed_visit_percent_smoothed | 18,028 | 237 | 0 | 2,376 | 3,951 | 0 |
| NSSP | participation_status | 2,756 | 0 | 3,180 | 0 | 0 | 0 |
| NWSS | participation_status | 1,555 | 0 | 288 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,572 | 0 | 0 | 271 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,571 | 1 | 0 | 271 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for TN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 62 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 80% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.27 |
| Wastewater: same, influenza A | 0.19 |
| Wastewater: same, RSV | 0.19 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`tn_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,879,572 rows covering 82,009 distinct values. Of those, 26,385 (32.2%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 3,500,189 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 64,833 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `tn_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `tn_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `tn_nssp_wide.csv` matches the long table | PASS | 73,564 cells; missing 0, unexpected 0, differing 0 |
| `tn_nwss_wide.csv` matches the long table | PASS | 5,529 cells; missing 0, unexpected 0, differing 0 |
| `tn_all_sources_wide.csv` matches the long table | PASS | 82,009 cells; missing 0, unexpected 0, differing 0 |
| `tn_all_sources_wide.csv` census columns match `tn_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
