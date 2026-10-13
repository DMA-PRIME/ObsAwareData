# Utah (UT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 49
- Emergency-department regions (CDC health service areas): 10
- Wastewater sampling sites: 34 (with COVID-19 data: 34; influenza A: 33; RSV: 33)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ut_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `ut_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `ut_long_latest_2022.csv` | 7,528 | 16 | 1.7 |
| `ut_long_latest_2023.csv` | 12,926 | 16 | 3.0 |
| `ut_long_latest_2024.csv` | 14,003 | 16 | 3.3 |
| `ut_long_latest_2025.csv` | 22,463 | 16 | 5.2 |
| `ut_long_latest_2026.csv` | 16,988 | 16 | 3.9 |
| `ut_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ut_nssp_wide.csv` | 2,310 | 30 | 0.9 |
| `ut_nwss_wide.csv` | 7,961 | 24 | 1.7 |
| `ut_all_sources_wide.csv` | 322 | 905 | 2.1 |
| `ut_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-05 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 10 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 10 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 10 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 10 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 34 | 2022-01-01 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 33 | 2022-09-24 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 33 | 2022-09-24 | 2026-10-03 |

## Reliability flags

Number of rows in `ut_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 685 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 573 | 107 | 0 | 59 | 18 | 209 |
| NHSN | hospital_reporting_count | 739 | 18 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,233 | 0 | 1,697 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 5,260 | 2,090 | 0 | 0 | 1,890 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,343 | 170 | 0 | 682 | 3,045 | 0 |
| NSSP | participation_status | 1,050 | 0 | 1,050 | 0 | 0 | 0 |
| NWSS | participation_status | 12,185 | 0 | 2,534 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 13,396 | 0 | 0 | 1,323 | 0 | 0 |
| NWSS | wastewater_activity_level | 13,396 | 0 | 0 | 1,323 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for UT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 40 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.97 |
| Wastewater: same, influenza A | 0.95 |
| Wastewater: same, RSV | 0.95 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ut_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,997,138 rows covering 74,565 distinct values. Of those, 20,927 (28.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,265,984 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 428,250 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ut_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ut_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ut_nssp_wide.csv` matches the long table | PASS | 27,510 cells; missing 0, unexpected 0, differing 0 |
| `ut_nwss_wide.csv` matches the long table | PASS | 44,157 cells; missing 0, unexpected 0, differing 0 |
| `ut_all_sources_wide.csv` matches the long table | PASS | 74,565 cells; missing 0, unexpected 0, differing 0 |
| `ut_all_sources_wide.csv` census columns match `ut_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
