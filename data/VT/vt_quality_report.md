# Vermont (VT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 50
- Emergency-department regions (CDC health service areas): 7
- Wastewater sampling sites: 14 (with COVID-19 data: 14; influenza A: 12; RSV: 12)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (90 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `vt_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `vt_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `vt_long_latest_2022.csv` | 2,245 | 15 | 0.5 |
| `vt_long_latest_2023.csv` | 7,208 | 15 | 1.6 |
| `vt_long_latest_2024.csv` | 7,487 | 15 | 1.7 |
| `vt_long_latest_2025.csv` | 7,865 | 15 | 1.7 |
| `vt_long_latest_2026.csv` | 8,256 | 15 | 1.8 |
| `vt_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `vt_nssp_wide.csv` | 1,696 | 30 | 0.6 |
| `vt_nwss_wide.csv` | 1,428 | 24 | 0.4 |
| `vt_all_sources_wide.csv` | 324 | 461 | 0.9 |
| `vt_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 7 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 7 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 7 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 7 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 14 | 2022-05-07 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 12 | 2023-03-04 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 12 | 2023-03-04 | 2026-10-17 |

## Reliability flags

Number of rows in `vt_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 689 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 485 | 226 | 0 | 32 | 20 | 209 |
| NHSN | hospital_reporting_count | 743 | 20 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 4,452 | 0 | 636 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 3,788 | 1,399 | 0 | 0 | 1,597 | 0 |
| NSSP | ed_visit_percent_smoothed | 4,399 | 243 | 0 | 545 | 1,597 | 0 |
| NSSP | participation_status | 1,060 | 0 | 424 | 0 | 0 | 0 |
| NWSS | participation_status | 3,365 | 0 | 189 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 3,098 | 0 | 0 | 456 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,098 | 0 | 0 | 456 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for VT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 8 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 109% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 44% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.28 |
| Wastewater: same, influenza A | 0.94 |
| Wastewater: same, RSV | 0.93 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`vt_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,380,563 rows covering 33,718 distinct values. Of those, 8,725 (25.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 958,265 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 107,748 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `vt_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `vt_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `vt_nssp_wide.csv` matches the long table | PASS | 20,140 cells; missing 0, unexpected 0, differing 0 |
| `vt_nwss_wide.csv` matches the long table | PASS | 10,662 cells; missing 0, unexpected 0, differing 0 |
| `vt_all_sources_wide.csv` matches the long table | PASS | 33,718 cells; missing 0, unexpected 0, differing 0 |
| `vt_all_sources_wide.csv` census columns match `vt_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
