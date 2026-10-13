# Tennessee (TN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 47
- Emergency-department regions (CDC health service areas): 28
- Wastewater sampling sites: 10 (with COVID-19 data: 10; influenza A: 4; RSV: 4)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `tn_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `tn_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `tn_long_latest_2022.csv` | 5,995 | 16 | 1.5 |
| `tn_long_latest_2023.csv` | 20,063 | 16 | 5.1 |
| `tn_long_latest_2024.csv` | 20,147 | 16 | 5.2 |
| `tn_long_latest_2025.csv` | 19,439 | 16 | 5.0 |
| `tn_long_latest_2026.csv` | 14,586 | 16 | 3.7 |
| `tn_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `tn_nssp_wide.csv` | 6,061 | 30 | 2.3 |
| `tn_nwss_wide.csv` | 1,026 | 24 | 0.2 |
| `tn_all_sources_wide.csv` | 321 | 845 | 2.1 |
| `tn_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-28 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 29 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 29 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 29 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 29 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 10 | 2022-01-01 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 4 | 2023-06-17 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 4 | 2023-06-17 | 2026-09-26 |

## Reliability flags

Number of rows in `tn_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 678 | 0 | 76 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 686 | 6 | 0 | 45 | 17 | 209 |
| NHSN | hospital_reporting_count | 737 | 17 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 17,544 | 0 | 639 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 17,122 | 4,106 | 0 | 0 | 3,016 | 0 |
| NSSP | ed_visit_percent_smoothed | 17,814 | 262 | 0 | 2,316 | 3,852 | 0 |
| NSSP | participation_status | 2,717 | 0 | 3,135 | 0 | 0 | 0 |
| NWSS | participation_status | 1,596 | 0 | 229 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,519 | 0 | 0 | 306 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,518 | 1 | 0 | 306 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for TN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 62 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 80% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.27 |
| Wastewater: same, influenza A | 0.19 |
| Wastewater: same, RSV | 0.19 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`tn_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,626,195 rows covering 80,887 distinct values. Of those, 25,538 (31.6%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 3,280,538 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 48,549 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `tn_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `tn_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `tn_nssp_wide.csv` matches the long table | PASS | 72,523 cells; missing 0, unexpected 0, differing 0 |
| `tn_nwss_wide.csv` matches the long table | PASS | 5,475 cells; missing 0, unexpected 0, differing 0 |
| `tn_all_sources_wide.csv` matches the long table | PASS | 80,887 cells; missing 0, unexpected 0, differing 0 |
| `tn_all_sources_wide.csv` census columns match `tn_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
