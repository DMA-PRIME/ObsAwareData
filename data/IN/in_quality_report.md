# Indiana (IN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 18
- Emergency-department regions (CDC health service areas): 29
- Wastewater sampling sites: 35 (with COVID-19 data: 35; influenza A: 30; RSV: 30)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `in_long_latest.csv` | 109,943 | 17 | 36.8 |
| `in_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `in_nssp_wide.csv` | 6,060 | 30 | 2.3 |
| `in_nwss_wide.csv` | 5,290 | 24 | 1.3 |
| `in_all_sources_wide.csv` | 316 | 1,331 | 3.0 |
| `in_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 29 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 29 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 29 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 29 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 35 | 2022-05-07 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 30 | 2022-08-20 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 30 | 2022-08-20 | 2026-08-22 |

## Reliability flags

Number of rows in `in_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 661 | 18 | 0 | 43 | 11 | 209 |
| NHSN | hospital_reporting_count | 722 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 15,917 | 0 | 2,263 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 14,690 | 5,929 | 0 | 0 | 3,621 | 0 |
| NSSP | ed_visit_percent_smoothed | 16,392 | 587 | 0 | 1,919 | 5,342 | 0 |
| NSSP | participation_status | 1,616 | 0 | 4,242 | 0 | 0 | 0 |
| NWSS | participation_status | 10,090 | 0 | 1,443 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 10,352 | 0 | 0 | 1,181 | 0 | 0 |
| NWSS | wastewater_activity_level | 8,481 | 0 | 0 | 3,052 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 100 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 87% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`in_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,268,884 rows covering 109,943 distinct values. Of those, 28,346 (25.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 2,875,590 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 136,254 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `in_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `in_nssp_wide.csv` matches the long table | PASS | 72,518 cells; missing 0, unexpected 0, differing 0 |
| `in_nwss_wide.csv` matches the long table | PASS | 34,599 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` matches the long table | PASS | 109,943 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` census columns match `in_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
