# Maine (ME): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 23
- Emergency-department regions (CDC health service areas): 6
- Wastewater sampling sites: 30 (with COVID-19 data: 30; influenza A: 22; RSV: 16)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `me_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `me_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `me_long_latest_2022.csv` | 4,282 | 16 | 1.0 |
| `me_long_latest_2023.csv` | 9,362 | 16 | 2.2 |
| `me_long_latest_2024.csv` | 12,746 | 16 | 3.0 |
| `me_long_latest_2025.csv` | 12,470 | 16 | 2.9 |
| `me_long_latest_2026.csv` | 9,015 | 16 | 2.1 |
| `me_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `me_nssp_wide.csv` | 1,463 | 30 | 0.5 |
| `me_nwss_wide.csv` | 4,804 | 24 | 1.1 |
| `me_all_sources_wide.csv` | 321 | 617 | 1.4 |
| `me_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 7 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 7 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 7 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 7 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 30 | 2022-02-19 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 22 | 2022-09-03 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 16 | 2022-09-03 | 2026-09-26 |

## Reliability flags

Number of rows in `me_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 682 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 548 | 151 | 0 | 36 | 19 | 209 |
| NHSN | hospital_reporting_count | 735 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 4,389 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,159 | 965 | 0 | 0 | 728 | 0 |
| NSSP | ed_visit_percent_smoothed | 4,139 | 255 | 0 | 521 | 937 | 0 |
| NSSP | participation_status | 1,045 | 0 | 209 | 0 | 0 | 0 |
| NWSS | participation_status | 8,344 | 0 | 1,088 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 8,291 | 0 | 0 | 1,141 | 0 | 0 |
| NWSS | wastewater_activity_level | 8,291 | 0 | 0 | 1,141 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for ME |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 20 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 142% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.47 |
| Wastewater: same, influenza A | 0.72 |
| Wastewater: same, RSV | 0.66 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`me_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,329,773 rows covering 48,532 distinct values. Of those, 13,534 (27.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 784,682 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 247,983 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `me_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `me_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `me_nssp_wide.csv` matches the long table | PASS | 17,347 cells; missing 0, unexpected 0, differing 0 |
| `me_nwss_wide.csv` matches the long table | PASS | 28,296 cells; missing 0, unexpected 0, differing 0 |
| `me_all_sources_wide.csv` matches the long table | PASS | 48,532 cells; missing 0, unexpected 0, differing 0 |
| `me_all_sources_wide.csv` census columns match `me_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
