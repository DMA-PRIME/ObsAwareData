# West Virginia (WV): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 54
- Emergency-department regions (CDC health service areas): 16
- Wastewater sampling sites: 35 (with COVID-19 data: 35; influenza A: 28; RSV: 24)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wv_long_latest.csv` | 71,198 | 17 | 23.8 |
| `wv_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `wv_nssp_wide.csv` | 3,434 | 30 | 1.3 |
| `wv_nwss_wide.csv` | 5,384 | 24 | 1.2 |
| `wv_all_sources_wide.csv` | 316 | 969 | 2.0 |
| `wv_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 16 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 16 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 16 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 16 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 35 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 28 | 2023-04-15 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 24 | 2023-04-15 | 2026-08-22 |

## Reliability flags

Number of rows in `wv_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 566 | 102 | 0 | 35 | 30 | 209 |
| NHSN | hospital_reporting_count | 703 | 30 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 9,090 | 0 | 1,212 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 8,772 | 2,604 | 0 | 0 | 2,360 | 0 |
| NSSP | ed_visit_percent_smoothed | 9,578 | 259 | 0 | 1,135 | 2,764 | 0 |
| NSSP | participation_status | 1,010 | 0 | 2,222 | 0 | 0 | 0 |
| NWSS | participation_status | 8,155 | 0 | 961 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 8,662 | 0 | 0 | 463 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,525 | 29 | 0 | 2,571 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WV |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 24 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 109% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.45 |
| Wastewater: same, influenza A | 0.44 |
| Wastewater: same, RSV | 0.50 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`wv_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,986,105 rows covering 71,198 distinct values. Of those, 20,283 (28.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 1,626,030 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 103,035 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wv_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `wv_nssp_wide.csv` matches the long table | PASS | 41,006 cells; missing 0, unexpected 0, differing 0 |
| `wv_nwss_wide.csv` matches the long table | PASS | 27,366 cells; missing 0, unexpected 0, differing 0 |
| `wv_all_sources_wide.csv` matches the long table | PASS | 71,198 cells; missing 0, unexpected 0, differing 0 |
| `wv_all_sources_wide.csv` census columns match `wv_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
