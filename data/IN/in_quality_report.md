# Indiana (IN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 18
- Emergency-department regions (CDC health service areas): 29
- Wastewater sampling sites: 35 (with COVID-19 data: 35; influenza A: 30; RSV: 30)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `in_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `in_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `in_long_latest_2022.csv` | 7,768 | 16 | 1.9 |
| `in_long_latest_2023.csv` | 24,056 | 16 | 6.0 |
| `in_long_latest_2024.csv` | 25,802 | 16 | 6.4 |
| `in_long_latest_2025.csv` | 31,688 | 16 | 7.8 |
| `in_long_latest_2026.csv` | 23,739 | 16 | 5.8 |
| `in_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `in_nssp_wide.csv` | 6,270 | 30 | 2.4 |
| `in_nwss_wide.csv` | 5,424 | 24 | 1.3 |
| `in_all_sources_wide.csv` | 321 | 1,331 | 3.1 |
| `in_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 29 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 29 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 29 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 29 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 35 | 2022-05-07 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 30 | 2022-08-20 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 30 | 2022-08-20 | 2026-09-26 |

## Reliability flags

Number of rows in `in_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 681 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 676 | 18 | 0 | 49 | 11 | 209 |
| NHSN | hospital_reporting_count | 743 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 15,465 | 0 | 3,344 | 0 | 1 | 0 |
| NSSP | ed_visit_percent | 14,962 | 6,266 | 0 | 0 | 3,852 | 0 |
| NSSP | ed_visit_percent_smoothed | 16,891 | 563 | 0 | 1,996 | 5,630 | 0 |
| NSSP | participation_status | 1,672 | 0 | 4,389 | 0 | 0 | 0 |
| NWSS | participation_status | 10,460 | 0 | 1,470 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 10,028 | 0 | 0 | 1,902 | 0 | 0 |
| NWSS | wastewater_activity_level | 10,028 | 0 | 0 | 1,902 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 100 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 87% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`in_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,003,907 rows covering 113,710 distinct values. Of those, 30,400 (26.7%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 3,393,986 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 312,813 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `in_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `in_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `in_nssp_wide.csv` matches the long table | PASS | 75,031 cells; missing 0, unexpected 0, differing 0 |
| `in_nwss_wide.csv` matches the long table | PASS | 35,790 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` matches the long table | PASS | 113,710 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` census columns match `in_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
