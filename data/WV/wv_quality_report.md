# West Virginia (WV): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 54
- Emergency-department regions (CDC health service areas): 16
- Wastewater sampling sites: 35 (with COVID-19 data: 35; influenza A: 28; RSV: 24)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-07 (79 releases); ED visits 2025-08-15 to 2026-10-07 (48 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wv_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `wv_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `wv_long_latest_2022.csv` | 6,676 | 15 | 1.5 |
| `wv_long_latest_2023.csv` | 15,350 | 15 | 3.7 |
| `wv_long_latest_2024.csv` | 17,186 | 15 | 4.1 |
| `wv_long_latest_2025.csv` | 19,112 | 15 | 4.5 |
| `wv_long_latest_2026.csv` | 14,771 | 15 | 3.5 |
| `wv_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `wv_nssp_wide.csv` | 3,570 | 30 | 1.4 |
| `wv_nwss_wide.csv` | 5,476 | 24 | 1.2 |
| `wv_all_sources_wide.csv` | 322 | 971 | 2.0 |
| `wv_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 16 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 16 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 16 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 16 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 35 | 2022-01-01 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 28 | 2023-04-15 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 24 | 2023-04-15 | 2026-10-03 |

## Reliability flags

Number of rows in `wv_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 683 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 586 | 103 | 0 | 38 | 30 | 209 |
| NHSN | hospital_reporting_count | 727 | 30 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 10,038 | 0 | 672 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 8,989 | 2,771 | 0 | 0 | 2,520 | 0 |
| NSSP | ed_visit_percent_smoothed | 9,863 | 252 | 0 | 1,225 | 2,940 | 0 |
| NSSP | participation_status | 1,050 | 0 | 2,310 | 0 | 0 | 0 |
| NWSS | participation_status | 8,361 | 0 | 1,047 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 8,337 | 0 | 0 | 1,071 | 0 | 0 |
| NWSS | wastewater_activity_level | 8,337 | 0 | 0 | 1,071 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,535,302 rows covering 73,752 distinct values. Of those, 22,610 (30.7%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,961,792 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 270,606 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `wv_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wv_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `wv_nssp_wide.csv` matches the long table | PASS | 42,630 cells; missing 0, unexpected 0, differing 0 |
| `wv_nwss_wide.csv` matches the long table | PASS | 28,224 cells; missing 0, unexpected 0, differing 0 |
| `wv_all_sources_wide.csv` matches the long table | PASS | 73,752 cells; missing 0, unexpected 0, differing 0 |
| `wv_all_sources_wide.csv` census columns match `wv_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
