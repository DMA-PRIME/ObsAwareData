# South Carolina (SC): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 45
- Emergency-department regions (CDC health service areas): 14
- Wastewater sampling sites: 31 (with COVID-19 data: 31; influenza A: 28; RSV: 26)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `sc_long_latest.csv` | 62,441 | 17 | 21.2 |
| `sc_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `sc_nssp_wide.csv` | 3,030 | 30 | 1.2 |
| `sc_nwss_wide.csv` | 3,473 | 24 | 0.9 |
| `sc_all_sources_wide.csv` | 316 | 911 | 1.8 |
| `sc_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 14 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 14 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 14 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 14 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 31 | 2022-01-08 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 28 | 2024-01-06 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 26 | 2024-01-06 | 2026-08-22 |

## Reliability flags

Number of rows in `sc_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 653 | 38 | 0 | 42 | 0 | 209 |
| NHSN | hospital_reporting_count | 733 | 0 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 7,878 | 0 | 1,212 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 8,342 | 1,612 | 0 | 0 | 2,166 | 0 |
| NSSP | ed_visit_percent_smoothed | 8,422 | 121 | 0 | 1,007 | 2,570 | 0 |
| NSSP | participation_status | 808 | 0 | 2,020 | 0 | 0 | 0 |
| NWSS | participation_status | 6,749 | 0 | 1,070 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 7,766 | 0 | 0 | 53 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,447 | 0 | 0 | 1,372 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for SC |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 50 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.75 |
| Wastewater: same, influenza A | 0.76 |
| Wastewater: same, RSV | 0.76 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`sc_long_all_versions.csv.gz`)

Location: in this folder.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,783,236 rows covering 62,441 distinct values. Of those, 14,883 (23.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 1,433,790 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 92,406 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `sc_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `sc_nssp_wide.csv` matches the long table | PASS | 36,158 cells; missing 0, unexpected 0, differing 0 |
| `sc_nwss_wide.csv` matches the long table | PASS | 23,457 cells; missing 0, unexpected 0, differing 0 |
| `sc_all_sources_wide.csv` matches the long table | PASS | 62,441 cells; missing 0, unexpected 0, differing 0 |
| `sc_all_sources_wide.csv` census columns match `sc_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
