# Oregon (OR): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 41
- Emergency-department regions (CDC health service areas): 14
- Wastewater sampling sites: 38 (with COVID-19 data: 38; influenza A: 38; RSV: 37)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-08-07, 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `or_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `or_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `or_long_latest_2022.csv` | 12,661 | 16 | 2.9 |
| `or_long_latest_2023.csv` | 19,469 | 16 | 4.6 |
| `or_long_latest_2024.csv` | 22,541 | 16 | 5.3 |
| `or_long_latest_2025.csv` | 23,861 | 16 | 5.6 |
| `or_long_latest_2026.csv` | 16,833 | 16 | 4.0 |
| `or_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `or_nssp_wide.csv` | 3,135 | 30 | 1.2 |
| `or_nwss_wide.csv` | 7,417 | 24 | 2.0 |
| `or_all_sources_wide.csv` | 321 | 1,079 | 2.6 |
| `or_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 15 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 15 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 15 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 15 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 38 | 2022-01-01 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 38 | 2022-01-01 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 37 | 2022-09-03 | 2026-09-26 |

## Reliability flags

Number of rows in `or_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 681 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 620 | 68 | 0 | 47 | 19 | 209 |
| NHSN | hospital_reporting_count | 735 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 8,759 | 0 | 646 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 8,131 | 2,849 | 0 | 0 | 1,560 | 0 |
| NSSP | ed_visit_percent_smoothed | 8,573 | 496 | 0 | 1,075 | 2,396 | 0 |
| NSSP | participation_status | 2,299 | 0 | 627 | 0 | 0 | 0 |
| NWSS | participation_status | 16,112 | 0 | 2,462 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 17,478 | 0 | 0 | 1,096 | 0 | 0 |
| NWSS | wastewater_activity_level | 17,478 | 0 | 0 | 1,096 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,481,998 rows covering 96,022 distinct values. Of those, 31,951 (33.3%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 1,692,266 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 492,624 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `or_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `or_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `or_nssp_wide.csv` matches the long table | PASS | 37,411 cells; missing 0, unexpected 0, differing 0 |
| `or_nwss_wide.csv` matches the long table | PASS | 55,722 cells; missing 0, unexpected 0, differing 0 |
| `or_all_sources_wide.csv` matches the long table | PASS | 96,022 cells; missing 0, unexpected 0, differing 0 |
| `or_all_sources_wide.csv` census columns match `or_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
