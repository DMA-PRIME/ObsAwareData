# Kentucky (KY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 21
- Emergency-department regions (CDC health service areas): 31
- Wastewater sampling sites: 33 (with COVID-19 data: 33; influenza A: 20; RSV: 10)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ky_long_latest.csv` | 95,971 | 17 | 32.7 |
| `ky_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ky_nssp_wide.csv` | 6,464 | 30 | 2.5 |
| `ky_nwss_wide.csv` | 2,254 | 24 | 0.6 |
| `ky_all_sources_wide.csv` | 316 | 1,179 | 2.5 |
| `ky_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 30 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 30 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 30 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 30 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 33 | 2022-02-26 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 20 | 2022-03-05 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 10 | 2022-03-05 | 2026-08-22 |

## Reliability flags

Number of rows in `ky_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 640 | 29 | 0 | 53 | 11 | 209 |
| NHSN | hospital_reporting_count | 722 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 17,285 | 0 | 2,107 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 16,146 | 5,184 | 0 | 0 | 4,526 | 0 |
| NSSP | ed_visit_percent_smoothed | 17,669 | 484 | 0 | 2,167 | 5,536 | 0 |
| NSSP | participation_status | 1,616 | 0 | 4,646 | 0 | 0 | 0 |
| NWSS | participation_status | 4,540 | 0 | 693 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 4,976 | 0 | 0 | 297 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,840 | 0 | 0 | 1,433 | 0 | 0 |

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

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ky_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ky_nssp_wide.csv` matches the long table | PASS | 77,366 cells; missing 0, unexpected 0, differing 0 |
| `ky_nwss_wide.csv` matches the long table | PASS | 15,779 cells; missing 0, unexpected 0, differing 0 |
| `ky_all_sources_wide.csv` matches the long table | PASS | 95,971 cells; missing 0, unexpected 0, differing 0 |
| `ky_all_sources_wide.csv` census columns match `ky_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
