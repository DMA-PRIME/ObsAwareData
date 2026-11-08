# West Virginia (WV): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 54
- Emergency-department regions (CDC health service areas): 16
- Wastewater sampling sites: 35 (with COVID-19 data: 35; influenza A: 28; RSV: 24)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-04 (83 releases); ED visits 2025-08-15 to 2026-11-04 (52 releases); wastewater 2026-08-07 to 2026-11-06 (14 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wv_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `wv_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `wv_long_latest_2022.csv` | 6,676 | 15 | 1.5 |
| `wv_long_latest_2023.csv` | 15,350 | 15 | 3.7 |
| `wv_long_latest_2024.csv` | 17,186 | 15 | 4.1 |
| `wv_long_latest_2025.csv` | 19,112 | 15 | 4.5 |
| `wv_long_latest_2026.csv` | 16,573 | 15 | 3.9 |
| `wv_nhsn_wide.csv` | 326 | 24 | 0.1 |
| `wv_nssp_wide.csv` | 3,638 | 30 | 1.4 |
| `wv_nwss_wide.csv` | 5,604 | 24 | 1.2 |
| `wv_all_sources_wide.csv` | 326 | 971 | 2.1 |
| `wv_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-31 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-31 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-31 |
| Emergency department visits (NSSP) | covid | 16 | 2022-10-01 | 2026-10-31 |
| Emergency department visits (NSSP) | influenza | 16 | 2022-10-01 | 2026-10-31 |
| Emergency department visits (NSSP) | rsv | 16 | 2022-10-01 | 2026-10-31 |
| Emergency department visits (NSSP) | combined | 16 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 35 | 2022-01-01 | 2026-10-31 |
| Wastewater (NWSS) | influenza | 28 | 2023-04-15 | 2026-10-31 |
| Wastewater (NWSS) | rsv | 24 | 2023-04-15 | 2026-10-31 |

## Reliability flags

Number of rows in `wv_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 695 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 597 | 103 | 0 | 39 | 30 | 209 |
| NHSN | hospital_reporting_count | 739 | 30 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 10,230 | 0 | 684 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 9,127 | 2,825 | 0 | 0 | 2,600 | 0 |
| NSSP | ed_visit_percent_smoothed | 10,098 | 220 | 0 | 1,206 | 3,028 | 0 |
| NSSP | participation_status | 1,070 | 0 | 2,354 | 0 | 0 | 0 |
| NWSS | participation_status | 8,661 | 0 | 1,065 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 8,526 | 0 | 0 | 1,200 | 0 | 0 |
| NWSS | wastewater_activity_level | 8,526 | 0 | 0 | 1,200 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WV |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 24 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 109% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.45 |
| Wastewater: same, influenza A | 0.44 |
| Wastewater: same, RSV | 0.50 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`wv_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,846,848 rows covering 75,554 distinct values. Of those, 23,829 (31.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 124 | 2025-04-04 | 2026-11-06 | 326,268 |
| NSSP | 57 | 2025-08-15 | 2026-11-04 | 2,134,342 |
| NWSS | 14 | 2026-08-07 | 2026-11-06 | 386,238 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `wv_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wv_nhsn_wide.csv` matches the long table | PASS | 2,934 cells; missing 0, unexpected 0, differing 0 |
| `wv_nssp_wide.csv` matches the long table | PASS | 43,442 cells; missing 0, unexpected 0, differing 0 |
| `wv_nwss_wide.csv` matches the long table | PASS | 29,178 cells; missing 0, unexpected 0, differing 0 |
| `wv_all_sources_wide.csv` matches the long table | PASS | 75,554 cells; missing 0, unexpected 0, differing 0 |
| `wv_all_sources_wide.csv` census columns match `wv_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 326 weeks, 2020-08-08 to 2026-10-31 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
