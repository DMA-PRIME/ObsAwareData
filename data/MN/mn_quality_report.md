# Minnesota (MN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 27
- Emergency-department regions (CDC health service areas): 26
- Wastewater sampling sites: 39 (with COVID-19 data: 39; influenza A: 26; RSV: 23)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mn_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `mn_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `mn_long_latest_2022.csv` | 9,016 | 16 | 2.2 |
| `mn_long_latest_2023.csv` | 23,318 | 16 | 5.8 |
| `mn_long_latest_2024.csv` | 23,519 | 16 | 5.9 |
| `mn_long_latest_2025.csv` | 25,610 | 16 | 6.4 |
| `mn_long_latest_2026.csv` | 21,457 | 16 | 5.3 |
| `mn_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `mn_nssp_wide.csv` | 5,643 | 30 | 2.2 |
| `mn_nwss_wide.csv` | 7,104 | 24 | 1.4 |
| `mn_all_sources_wide.csv` | 321 | 1,213 | 2.8 |
| `mn_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-07 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 22 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 22 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 22 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 22 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 39 | 2022-04-16 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 26 | 2022-09-03 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 23 | 2022-09-03 | 2026-09-26 |

## Reliability flags

Number of rows in `mn_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 682 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 598 | 64 | 0 | 46 | 46 | 209 |
| NHSN | hospital_reporting_count | 708 | 46 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 11,928 | 0 | 5,001 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 9,854 | 6,250 | 0 | 0 | 6,468 | 0 |
| NSSP | ed_visit_percent_smoothed | 11,162 | 577 | 0 | 1,334 | 9,499 | 0 |
| NSSP | participation_status | 4,180 | 0 | 1,254 | 0 | 0 | 0 |
| NWSS | participation_status | 9,792 | 0 | 1,255 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 9,338 | 0 | 0 | 1,729 | 0 | 0 |
| NWSS | wastewater_activity_level | 9,338 | 0 | 0 | 1,729 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 52 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.70 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.98 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`mn_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,639,429 rows covering 103,577 distinct values. Of those, 28,275 (27.3%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 3,053,642 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 288,679 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `mn_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mn_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `mn_nssp_wide.csv` matches the long table | PASS | 67,507 cells; missing 0, unexpected 0, differing 0 |
| `mn_nwss_wide.csv` matches the long table | PASS | 33,181 cells; missing 0, unexpected 0, differing 0 |
| `mn_all_sources_wide.csv` matches the long table | PASS | 103,577 cells; missing 0, unexpected 0, differing 0 |
| `mn_all_sources_wide.csv` census columns match `mn_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
