# Nevada (NV): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 32
- Emergency-department regions (CDC health service areas): 4
- Wastewater sampling sites: 10 (with COVID-19 data: 10; influenza A: 7; RSV: 7)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nv_long_latest.csv` | 21,197 | 17 | 6.9 |
| `nv_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `nv_nssp_wide.csv` | 1,010 | 30 | 0.4 |
| `nv_nwss_wide.csv` | 929 | 24 | 0.2 |
| `nv_all_sources_wide.csv` | 316 | 305 | 0.6 |
| `nv_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-05 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 5 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 5 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 5 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 5 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 10 | 2022-04-30 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 7 | 2023-04-01 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 7 | 2023-04-01 | 2026-08-22 |

## Reliability flags

Number of rows in `nv_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 613 | 56 | 0 | 50 | 14 | 209 |
| NHSN | hospital_reporting_count | 719 | 14 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 2,828 | 0 | 202 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 2,843 | 712 | 0 | 0 | 485 | 0 |
| NSSP | ed_visit_percent_smoothed | 2,884 | 48 | 0 | 421 | 687 | 0 |
| NSSP | participation_status | 202 | 0 | 606 | 0 | 0 | 0 |
| NWSS | participation_status | 1,841 | 0 | 310 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,751 | 0 | 0 | 400 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,487 | 0 | 0 | 664 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NV |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 39 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.31 |
| Wastewater: same, influenza A | 1.00 |
| Wastewater: same, RSV | 1.00 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`nv_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 755,064 rows covering 21,197 distinct values. Of those, 5,568 (26.3%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 472,590 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 25,434 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nv_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `nv_nssp_wide.csv` matches the long table | PASS | 11,918 cells; missing 0, unexpected 0, differing 0 |
| `nv_nwss_wide.csv` matches the long table | PASS | 6,453 cells; missing 0, unexpected 0, differing 0 |
| `nv_all_sources_wide.csv` matches the long table | PASS | 21,197 cells; missing 0, unexpected 0, differing 0 |
| `nv_all_sources_wide.csv` census columns match `nv_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
