# Georgia (GA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 13
- Emergency-department regions (CDC health service areas): 42
- Wastewater sampling sites: 30 (with COVID-19 data: 30; influenza A: 29; RSV: 28)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-08-07, 2026-09-11, 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ga_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `ga_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `ga_long_latest_2022.csv` | 9,817 | 16 | 2.5 |
| `ga_long_latest_2023.csv` | 33,098 | 16 | 8.4 |
| `ga_long_latest_2024.csv` | 35,801 | 16 | 9.0 |
| `ga_long_latest_2025.csv` | 36,101 | 16 | 9.1 |
| `ga_long_latest_2026.csv` | 28,292 | 16 | 7.1 |
| `ga_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ga_nssp_wide.csv` | 9,030 | 30 | 3.6 |
| `ga_nwss_wide.csv` | 4,484 | 24 | 1.2 |
| `ga_all_sources_wide.csv` | 322 | 1,595 | 3.8 |
| `ga_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-09-05 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 37 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 37 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 37 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 37 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 30 | 2022-04-16 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 29 | 2022-07-02 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 28 | 2022-07-02 | 2026-10-03 |

## Reliability flags

Number of rows in `ga_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 683 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 690 | 19 | 0 | 44 | 4 | 209 |
| NHSN | hospital_reporting_count | 753 | 4 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 19,076 | 0 | 8,014 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 18,839 | 8,356 | 0 | 0 | 8,925 | 0 |
| NSSP | ed_visit_percent_smoothed | 19,481 | 422 | 0 | 2,357 | 13,860 | 0 |
| NSSP | participation_status | 1,470 | 0 | 7,350 | 0 | 0 | 0 |
| NWSS | participation_status | 9,993 | 0 | 913 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 10,276 | 0 | 0 | 630 | 0 | 0 |
| NWSS | wastewater_activity_level | 10,276 | 0 | 0 | 630 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for GA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 91 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 72% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.57 |
| Wastewater: same, influenza A | 0.60 |
| Wastewater: same, RSV | 0.45 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ga_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 5,595,287 rows covering 143,766 distinct values. Of those, 33,732 (23.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 4,976,960 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 315,423 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ga_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ga_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ga_nssp_wide.csv` matches the long table | PASS | 108,150 cells; missing 0, unexpected 0, differing 0 |
| `ga_nwss_wide.csv` matches the long table | PASS | 32,718 cells; missing 0, unexpected 0, differing 0 |
| `ga_all_sources_wide.csv` matches the long table | PASS | 143,766 cells; missing 0, unexpected 0, differing 0 |
| `ga_all_sources_wide.csv` census columns match `ga_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
