# Kentucky (KY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 21
- Emergency-department regions (CDC health service areas): 31
- Wastewater sampling sites: 34 (with COVID-19 data: 34; influenza A: 21; RSV: 14)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-13 (103 releases); ED visits 2025-08-15 to 2026-11-12 (53 releases); wastewater 2026-08-07 to 2026-11-13 (15 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ky_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ky_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ky_long_latest_2022.csv` | 6,556 | 15 | 1.6 |
| `ky_long_latest_2023.csv` | 21,062 | 15 | 5.2 |
| `ky_long_latest_2024.csv` | 24,218 | 15 | 5.9 |
| `ky_long_latest_2025.csv` | 26,732 | 15 | 6.4 |
| `ky_long_latest_2026.csv` | 23,724 | 15 | 5.7 |
| `ky_nhsn_wide.csv` | 327 | 24 | 0.1 |
| `ky_nssp_wide.csv` | 6,880 | 30 | 2.7 |
| `ky_nwss_wide.csv` | 2,478 | 24 | 0.6 |
| `ky_all_sources_wide.csv` | 327 | 1,223 | 2.7 |
| `ky_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-11-07 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-11-07 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-11-07 |
| Emergency department visits (NSSP) | covid | 30 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | influenza | 30 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | rsv | 30 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | combined | 30 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 34 | 2022-02-26 | 2026-11-07 |
| Wastewater (NWSS) | influenza | 21 | 2022-03-05 | 2026-11-07 |
| Wastewater (NWSS) | rsv | 14 | 2022-03-05 | 2026-11-07 |

## Reliability flags

Number of rows in `ky_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 698 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 672 | 29 | 0 | 60 | 11 | 209 |
| NHSN | hospital_reporting_count | 761 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 18,615 | 0 | 2,025 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 16,862 | 5,638 | 0 | 0 | 5,020 | 0 |
| NSSP | ed_visit_percent_smoothed | 18,114 | 361 | 0 | 2,305 | 6,740 | 0 |
| NSSP | participation_status | 1,720 | 0 | 4,945 | 0 | 0 | 0 |
| NWSS | participation_status | 5,439 | 0 | 448 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 5,036 | 0 | 0 | 851 | 0 | 0 |
| NWSS | wastewater_activity_level | 5,036 | 0 | 0 | 851 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for KY |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 34 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 38% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.03 |
| Wastewater: same, influenza A | 0.90 |
| Wastewater: same, RSV | 0.92 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ky_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,687,076 rows covering 102,949 distinct values. Of those, 32,323 (31.4%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 126 | 2025-04-04 | 2026-11-13 | 332,154 |
| NSSP | 58 | 2025-08-15 | 2026-11-12 | 4,109,207 |
| NWSS | 15 | 2026-08-07 | 2026-11-13 | 245,715 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ky_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ky_nhsn_wide.csv` matches the long table | PASS | 2,943 cells; missing 0, unexpected 0, differing 0 |
| `ky_nssp_wide.csv` matches the long table | PASS | 82,345 cells; missing 0, unexpected 0, differing 0 |
| `ky_nwss_wide.csv` matches the long table | PASS | 17,661 cells; missing 0, unexpected 0, differing 0 |
| `ky_all_sources_wide.csv` matches the long table | PASS | 102,949 cells; missing 0, unexpected 0, differing 0 |
| `ky_all_sources_wide.csv` census columns match `ky_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 327 weeks, 2020-08-08 to 2026-11-07 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
