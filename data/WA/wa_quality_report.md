# Washington (WA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 53
- Emergency-department regions (CDC health service areas): 15
- Wastewater sampling sites: 32 (with COVID-19 data: 32; influenza A: 29; RSV: 29)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wa_long_latest.csv` | 77,411 | 17 | 25.5 |
| `wa_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `wa_nssp_wide.csv` | 3,232 | 30 | 1.3 |
| `wa_nwss_wide.csv` | 5,726 | 24 | 1.4 |
| `wa_all_sources_wide.csv` | 316 | 965 | 2.2 |
| `wa_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 32 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 29 | 2023-08-19 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 29 | 2023-08-19 | 2026-08-22 |

## Reliability flags

Number of rows in `wa_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 662 | 0 | 71 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 634 | 53 | 0 | 41 | 5 | 209 |
| NHSN | hospital_reporting_count | 728 | 5 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 9,090 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 703 | 8 | 0 | 0 | 12,217 | 0 |
| NSSP | ed_visit_percent_smoothed | 634 | 1 | 0 | 76 | 12,217 | 0 |
| NSSP | participation_status | 2,424 | 0 | 606 | 0 | 0 | 0 |
| NWSS | participation_status | 9,686 | 0 | 2,315 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 11,997 | 0 | 0 | 4 | 0 | 0 |
| NWSS | wastewater_activity_level | 9,741 | 0 | 0 | 2,260 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 92 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 80% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 31% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.92 |
| Wastewater: same, influenza A | 0.93 |
| Wastewater: same, RSV | 0.47 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`wa_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,928,835 rows covering 77,411 distinct values. Of those, 9,847 (12.7%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 1,529,910 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 141,885 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wa_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `wa_nssp_wide.csv` matches the long table | PASS | 38,582 cells; missing 0, unexpected 0, differing 0 |
| `wa_nwss_wide.csv` matches the long table | PASS | 36,003 cells; missing 0, unexpected 0, differing 0 |
| `wa_all_sources_wide.csv` matches the long table | PASS | 77,411 cells; missing 0, unexpected 0, differing 0 |
| `wa_all_sources_wide.csv` census columns match `wa_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
