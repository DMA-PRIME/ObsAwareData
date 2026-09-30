# Maine (ME): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 23
- Emergency-department regions (CDC health service areas): 6
- Wastewater sampling sites: 30 (with COVID-19 data: 30; influenza A: 22; RSV: 16)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-21, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `me_long_latest.csv` | 47,003 | 17 | 15.0 |
| `me_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `me_nssp_wide.csv` | 1,414 | 30 | 0.5 |
| `me_nwss_wide.csv` | 4,720 | 24 | 1.0 |
| `me_all_sources_wide.csv` | 316 | 607 | 1.3 |
| `me_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 7 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 7 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 7 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 7 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 30 | 2022-02-19 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 22 | 2022-09-03 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 16 | 2022-09-03 | 2026-08-22 |

## Reliability flags

Number of rows in `me_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 661 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 541 | 140 | 0 | 33 | 19 | 209 |
| NHSN | hospital_reporting_count | 714 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 4,242 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,072 | 905 | 0 | 0 | 679 | 0 |
| NSSP | ed_visit_percent_smoothed | 4,049 | 230 | 0 | 496 | 881 | 0 |
| NSSP | participation_status | 1,010 | 0 | 202 | 0 | 0 | 0 |
| NWSS | participation_status | 7,885 | 0 | 1,076 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 8,817 | 0 | 0 | 408 | 0 | 0 |
| NWSS | wastewater_activity_level | 7,105 | 0 | 0 | 2,120 | 0 | 0 |

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

## Revision history (`me_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,028,540 rows covering 47,003 distinct values. Of those, 13,208 (28.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 664,830 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 106,670 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `me_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `me_nssp_wide.csv` matches the long table | PASS | 16,766 cells; missing 0, unexpected 0, differing 0 |
| `me_nwss_wide.csv` matches the long table | PASS | 27,411 cells; missing 0, unexpected 0, differing 0 |
| `me_all_sources_wide.csv` matches the long table | PASS | 47,003 cells; missing 0, unexpected 0, differing 0 |
| `me_all_sources_wide.csv` census columns match `me_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
