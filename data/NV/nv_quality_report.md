# Nevada (NV): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 32
- Emergency-department regions (CDC health service areas): 4
- Wastewater sampling sites: 10 (with COVID-19 data: 10; influenza A: 7; RSV: 7)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (93 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nv_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `nv_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `nv_long_latest_2022.csv` | 1,792 | 15 | 0.4 |
| `nv_long_latest_2023.csv` | 4,361 | 15 | 1.0 |
| `nv_long_latest_2024.csv` | 4,013 | 15 | 0.9 |
| `nv_long_latest_2025.csv` | 6,056 | 15 | 1.4 |
| `nv_long_latest_2026.csv` | 5,241 | 15 | 1.2 |
| `nv_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `nv_nssp_wide.csv` | 1,060 | 30 | 0.4 |
| `nv_nwss_wide.csv` | 956 | 24 | 0.3 |
| `nv_all_sources_wide.csv` | 324 | 305 | 0.6 |
| `nv_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-05 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 5 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 5 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 5 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 5 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 10 | 2022-04-30 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 7 | 2023-04-01 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 7 | 2023-04-01 | 2026-10-17 |

## Reliability flags

Number of rows in `nv_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 692 | 0 | 71 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 637 | 59 | 0 | 53 | 14 | 209 |
| NHSN | hospital_reporting_count | 749 | 14 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 2,756 | 0 | 424 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 2,939 | 766 | 0 | 0 | 535 | 0 |
| NSSP | ed_visit_percent_smoothed | 3,004 | 41 | 0 | 448 | 747 | 0 |
| NSSP | participation_status | 212 | 0 | 636 | 0 | 0 | 0 |
| NWSS | participation_status | 1,126 | 0 | 1,106 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,750 | 0 | 0 | 482 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,750 | 0 | 0 | 482 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NV |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 39 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.31 |
| Wastewater: same, influenza A | 1.00 |
| Wastewater: same, RSV | 1.00 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`nv_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 988,208 rows covering 22,120 distinct values. Of those, 6,975 (31.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 595,133 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 78,525 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `nv_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nv_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `nv_nssp_wide.csv` matches the long table | PASS | 12,508 cells; missing 0, unexpected 0, differing 0 |
| `nv_nwss_wide.csv` matches the long table | PASS | 6,696 cells; missing 0, unexpected 0, differing 0 |
| `nv_all_sources_wide.csv` matches the long table | PASS | 22,120 cells; missing 0, unexpected 0, differing 0 |
| `nv_all_sources_wide.csv` census columns match `nv_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
