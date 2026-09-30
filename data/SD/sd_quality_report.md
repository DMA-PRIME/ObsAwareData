# South Dakota (SD): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 46
- Emergency-department regions (CDC health service areas): 15
- Wastewater sampling sites: 6 (with COVID-19 data: 6; influenza A: 5; RSV: 5)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `sd_long_latest.csv` | 46,223 | 17 | 16.0 |
| `sd_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `sd_nssp_wide.csv` | 3,232 | 30 | 1.4 |
| `sd_nwss_wide.csv` | 687 | 24 | 0.2 |
| `sd_all_sources_wide.csv` | 316 | 521 | 1.3 |
| `sd_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-03 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 0 | none | none |
| Wastewater (NWSS) | covid | 6 | 2022-06-04 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 5 | 2023-04-29 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 5 | 2023-04-29 | 2026-08-22 |

## Reliability flags

Number of rows in `sd_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 575 | 115 | 0 | 35 | 8 | 209 |
| NHSN | hospital_reporting_count | 725 | 8 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 9,090 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 550 | 56 | 0 | 0 | 12,322 | 0 |
| NSSP | ed_visit_percent_smoothed | 514 | 25 | 0 | 67 | 12,322 | 0 |
| NSSP | participation_status | 1,010 | 0 | 2,020 | 0 | 0 | 0 |
| NWSS | participation_status | 1,412 | 0 | 193 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,605 | 0 | 0 | 0 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,382 | 0 | 0 | 223 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for SD |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 28 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 134% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 50% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.61 |
| Wastewater: same, influenza A | 0.86 |
| Wastewater: same, RSV | 0.86 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`sd_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,804,572 rows covering 46,223 distinct values. Of those, 2,362 (5.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 1,529,910 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 17,622 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `sd_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `sd_nssp_wide.csv` matches the long table | PASS | 38,582 cells; missing 0, unexpected 0, differing 0 |
| `sd_nwss_wide.csv` matches the long table | PASS | 4,815 cells; missing 0, unexpected 0, differing 0 |
| `sd_all_sources_wide.csv` matches the long table | PASS | 46,223 cells; missing 0, unexpected 0, differing 0 |
| `sd_all_sources_wide.csv` census columns match `sd_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
