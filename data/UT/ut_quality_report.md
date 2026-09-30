# Utah (UT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 49
- Emergency-department regions (CDC health service areas): 10
- Wastewater sampling sites: 34 (with COVID-19 data: 34; influenza A: 33; RSV: 33)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ut_long_latest.csv` | 71,681 | 17 | 22.9 |
| `ut_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ut_nssp_wide.csv` | 2,222 | 30 | 0.8 |
| `ut_nwss_wide.csv` | 7,765 | 24 | 1.7 |
| `ut_all_sources_wide.csv` | 316 | 905 | 2.0 |
| `ut_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-05 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 10 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 10 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 10 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 10 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 34 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 33 | 2022-09-24 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 33 | 2022-09-24 | 2026-08-22 |

## Reliability flags

Number of rows in `ut_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 661 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 555 | 102 | 0 | 58 | 18 | 209 |
| NHSN | hospital_reporting_count | 715 | 18 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,252 | 0 | 1,414 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 5,144 | 1,966 | 0 | 0 | 1,778 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,228 | 135 | 0 | 632 | 2,893 | 0 |
| NSSP | participation_status | 1,010 | 0 | 1,010 | 0 | 0 | 0 |
| NWSS | participation_status | 11,875 | 0 | 2,256 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 13,366 | 0 | 0 | 765 | 0 | 0 |
| NWSS | wastewater_activity_level | 10,879 | 0 | 0 | 3,252 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for UT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 40 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.97 |
| Wastewater: same, influenza A | 0.95 |
| Wastewater: same, RSV | 0.95 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ut_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,474,104 rows covering 71,681 distinct values. Of those, 18,945 (26.4%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 1,049,310 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 167,754 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ut_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ut_nssp_wide.csv` matches the long table | PASS | 26,462 cells; missing 0, unexpected 0, differing 0 |
| `ut_nwss_wide.csv` matches the long table | PASS | 42,393 cells; missing 0, unexpected 0, differing 0 |
| `ut_all_sources_wide.csv` matches the long table | PASS | 71,681 cells; missing 0, unexpected 0, differing 0 |
| `ut_all_sources_wide.csv` census columns match `ut_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
