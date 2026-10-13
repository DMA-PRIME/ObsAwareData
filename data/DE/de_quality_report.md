# Delaware (DE): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 10
- Emergency-department regions (CDC health service areas): 2
- Wastewater sampling sites: 9 (with COVID-19 data: 9; influenza A: 9; RSV: 8)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `de_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `de_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `de_long_latest_2022.csv` | 1,897 | 16 | 0.4 |
| `de_long_latest_2023.csv` | 4,772 | 16 | 1.1 |
| `de_long_latest_2024.csv` | 6,032 | 16 | 1.4 |
| `de_long_latest_2025.csv` | 5,441 | 16 | 1.2 |
| `de_long_latest_2026.csv` | 4,248 | 16 | 1.0 |
| `de_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `de_nssp_wide.csv` | 627 | 30 | 0.2 |
| `de_nwss_wide.csv` | 1,886 | 24 | 0.5 |
| `de_all_sources_wide.csv` | 321 | 269 | 0.7 |
| `de_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 3 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 3 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 3 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 3 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 9 | 2022-04-09 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 9 | 2023-02-11 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 8 | 2023-02-11 | 2026-09-26 |

## Reliability flags

Number of rows in `de_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 684 | 0 | 70 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 524 | 174 | 0 | 45 | 11 | 209 |
| NHSN | hospital_reporting_count | 743 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 1,881 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 2,095 | 101 | 0 | 0 | 312 | 0 |
| NSSP | ed_visit_percent_smoothed | 1,949 | 7 | 0 | 240 | 312 | 0 |
| NSSP | participation_status | 418 | 0 | 0 | 0 | 0 | 0 |
| NWSS | participation_status | 3,092 | 0 | 1,189 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 3,599 | 0 | 0 | 682 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,599 | 0 | 0 | 682 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for DE |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 7 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 38% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.99 |
| Wastewater: same, influenza A | 0.99 |
| Wastewater: same, RSV | 0.71 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`de_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 741,143 rows covering 23,047 distinct values. Of those, 6,935 (30.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 330,890 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 113,145 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `de_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `de_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `de_nssp_wide.csv` matches the long table | PASS | 7,315 cells; missing 0, unexpected 0, differing 0 |
| `de_nwss_wide.csv` matches the long table | PASS | 12,843 cells; missing 0, unexpected 0, differing 0 |
| `de_all_sources_wide.csv` matches the long table | PASS | 23,047 cells; missing 0, unexpected 0, differing 0 |
| `de_all_sources_wide.csv` census columns match `de_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
