# Kentucky (KY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 21
- Emergency-department regions (CDC health service areas): 31
- Wastewater sampling sites: 34 (with COVID-19 data: 34; influenza A: 21; RSV: 13)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ky_long_latest.csv` | 100,158 | 17 | 31.9 |
| `ky_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ky_nssp_wide.csv` | 6,720 | 30 | 2.6 |
| `ky_nwss_wide.csv` | 2,378 | 24 | 0.6 |
| `ky_all_sources_wide.csv` | 322 | 1,215 | 2.7 |
| `ky_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 30 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 30 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 30 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 30 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 34 | 2022-02-26 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 21 | 2022-03-05 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 13 | 2022-03-05 | 2026-10-03 |

## Reliability flags

Number of rows in `ky_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 683 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 658 | 29 | 0 | 59 | 11 | 209 |
| NHSN | hospital_reporting_count | 746 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 18,183 | 0 | 1,977 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 16,523 | 5,527 | 0 | 0 | 4,830 | 0 |
| NSSP | ed_visit_percent_smoothed | 17,955 | 400 | 0 | 2,225 | 6,300 | 0 |
| NSSP | participation_status | 1,680 | 0 | 4,830 | 0 | 0 | 0 |
| NWSS | participation_status | 5,061 | 0 | 543 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 5,215 | 0 | 0 | 398 | 0 | 0 |
| NWSS | wastewater_activity_level | 4,004 | 0 | 0 | 1,609 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for KY |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 34 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 38% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.03 |
| Wastewater: same, influenza A | 0.90 |
| Wastewater: same, RSV | 0.92 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ky_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,163,252 rows covering 100,158 distinct values. Of those, 29,161 (29.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 3,701,312 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 159,036 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ky_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ky_nssp_wide.csv` matches the long table | PASS | 80,430 cells; missing 0, unexpected 0, differing 0 |
| `ky_nwss_wide.csv` matches the long table | PASS | 16,830 cells; missing 0, unexpected 0, differing 0 |
| `ky_all_sources_wide.csv` matches the long table | PASS | 100,158 cells; missing 0, unexpected 0, differing 0 |
| `ky_all_sources_wide.csv` census columns match `ky_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
