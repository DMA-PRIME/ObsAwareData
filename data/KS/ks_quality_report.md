# Kansas (KS): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 20
- Emergency-department regions (CDC health service areas): 37
- Wastewater sampling sites: 15 (with COVID-19 data: 15; influenza A: 14; RSV: 14)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ks_long_latest.csv` | 116,108 | 17 | 38.4 |
| `ks_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ks_nssp_wide.csv` | 7,676 | 30 | 2.9 |
| `ks_nwss_wide.csv` | 2,764 | 24 | 0.7 |
| `ks_all_sources_wide.csv` | 316 | 1,211 | 3.0 |
| `ks_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 37 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 37 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 37 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 37 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 15 | 2022-05-07 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 14 | 2022-08-06 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 14 | 2022-08-06 | 2026-08-22 |

## Reliability flags

Number of rows in `ks_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 613 | 53 | 0 | 57 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 11,918 | 0 | 11,110 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 12,773 | 13,534 | 0 | 0 | 4,397 | 0 |
| NSSP | ed_visit_percent_smoothed | 14,245 | 428 | 0 | 1,728 | 14,303 | 0 |
| NSSP | participation_status | 5,252 | 0 | 2,222 | 0 | 0 | 0 |
| NWSS | participation_status | 6,052 | 0 | 1,072 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 6,169 | 0 | 0 | 955 | 0 | 0 |
| NWSS | wastewater_activity_level | 5,177 | 0 | 0 | 1,947 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for KS |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 79 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.96 |
| Wastewater: same, influenza A | 0.97 |
| Wastewater: same, RSV | 0.97 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ks_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,986,556 rows covering 116,108 distinct values. Of those, 24,736 (21.3%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 3,644,550 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 84,966 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ks_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ks_nssp_wide.csv` matches the long table | PASS | 91,910 cells; missing 0, unexpected 0, differing 0 |
| `ks_nwss_wide.csv` matches the long table | PASS | 21,372 cells; missing 0, unexpected 0, differing 0 |
| `ks_all_sources_wide.csv` matches the long table | PASS | 116,108 cells; missing 0, unexpected 0, differing 0 |
| `ks_all_sources_wide.csv` census columns match `ks_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
