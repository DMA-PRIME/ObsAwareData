# Arkansas (AR): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 05
- Emergency-department regions (CDC health service areas): 22
- Wastewater sampling sites: 21 (with COVID-19 data: 21; influenza A: 7; RSV: 7)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-08-07, 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ar_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `ar_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `ar_long_latest_2022.csv` | 5,317 | 16 | 1.3 |
| `ar_long_latest_2023.csv` | 17,339 | 16 | 4.4 |
| `ar_long_latest_2024.csv` | 17,405 | 16 | 4.4 |
| `ar_long_latest_2025.csv` | 17,558 | 16 | 4.4 |
| `ar_long_latest_2026.csv` | 13,313 | 16 | 3.4 |
| `ar_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ar_nssp_wide.csv` | 4,830 | 30 | 2.0 |
| `ar_nwss_wide.csv` | 1,904 | 24 | 0.4 |
| `ar_all_sources_wide.csv` | 322 | 803 | 2.1 |
| `ar_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 21 | 2022-06-11 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 7 | 2023-04-29 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 7 | 2023-04-29 | 2026-10-03 |

## Reliability flags

Number of rows in `ar_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 681 | 0 | 76 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 667 | 23 | 0 | 57 | 10 | 209 |
| NHSN | hospital_reporting_count | 747 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 630 | 0 | 13,860 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 734 | 1 | 0 | 0 | 18,585 | 0 |
| NSSP | ed_visit_percent_smoothed | 655 | 0 | 0 | 80 | 18,585 | 0 |
| NSSP | participation_status | 1,890 | 0 | 2,730 | 0 | 0 | 0 |
| NWSS | participation_status | 3,124 | 0 | 523 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 3,116 | 0 | 0 | 531 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,116 | 0 | 0 | 531 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for AR |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 55 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.22 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.91 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ar_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,068,573 rows covering 71,589 distinct values. Of those, 4,842 (6.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 2,657,600 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 108,069 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ar_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ar_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ar_nssp_wide.csv` matches the long table | PASS | 57,750 cells; missing 0, unexpected 0, differing 0 |
| `ar_nwss_wide.csv` matches the long table | PASS | 10,941 cells; missing 0, unexpected 0, differing 0 |
| `ar_all_sources_wide.csv` matches the long table | PASS | 71,589 cells; missing 0, unexpected 0, differing 0 |
| `ar_all_sources_wide.csv` census columns match `ar_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
