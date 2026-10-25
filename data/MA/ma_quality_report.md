# Massachusetts (MA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 25
- Emergency-department regions (CDC health service areas): 6
- Wastewater sampling sites: 12 (with COVID-19 data: 12; influenza A: 8; RSV: 8)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (83 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ma_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ma_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ma_long_latest_2022.csv` | 2,416 | 15 | 0.5 |
| `ma_long_latest_2023.csv` | 6,725 | 15 | 1.6 |
| `ma_long_latest_2024.csv` | 7,427 | 15 | 1.7 |
| `ma_long_latest_2025.csv` | 7,265 | 15 | 1.7 |
| `ma_long_latest_2026.csv` | 5,742 | 15 | 1.3 |
| `ma_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `ma_nssp_wide.csv` | 1,484 | 30 | 0.5 |
| `ma_nwss_wide.csv` | 1,689 | 24 | 0.4 |
| `ma_all_sources_wide.csv` | 324 | 377 | 0.8 |
| `ma_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 7 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 7 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 7 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 7 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 12 | 2022-01-01 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 8 | 2022-12-17 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 8 | 2022-12-17 | 2026-10-17 |

## Reliability flags

Number of rows in `ma_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 689 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 616 | 43 | 0 | 50 | 54 | 209 |
| NHSN | hospital_reporting_count | 709 | 54 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 4,452 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,869 | 318 | 0 | 0 | 749 | 0 |
| NSSP | ed_visit_percent_smoothed | 4,589 | 35 | 0 | 563 | 749 | 0 |
| NSSP | participation_status | 1,272 | 0 | 0 | 0 | 0 | 0 |
| NWSS | participation_status | 2,642 | 0 | 598 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 3,132 | 0 | 0 | 108 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,132 | 0 | 0 | 108 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 4 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.32 |
| Wastewater: same, influenza A | 0.75 |
| Wastewater: same, RSV | 0.75 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ma_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,264,082 rows covering 30,232 distinct values. Of those, 10,574 (35.0%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 837,221 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 112,311 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ma_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ma_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `ma_nssp_wide.csv` matches the long table | PASS | 17,596 cells; missing 0, unexpected 0, differing 0 |
| `ma_nwss_wide.csv` matches the long table | PASS | 9,720 cells; missing 0, unexpected 0, differing 0 |
| `ma_all_sources_wide.csv` matches the long table | PASS | 30,232 cells; missing 0, unexpected 0, differing 0 |
| `ma_all_sources_wide.csv` census columns match `ma_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
