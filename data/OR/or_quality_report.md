# Oregon (OR): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 41
- Emergency-department regions (CDC health service areas): 14
- Wastewater sampling sites: 38 (with COVID-19 data: 38; influenza A: 38; RSV: 37)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `or_long_latest.csv` | 93,125 | 17 | 30.0 |
| `or_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `or_nssp_wide.csv` | 3,030 | 30 | 1.1 |
| `or_nwss_wide.csv` | 7,232 | 24 | 1.9 |
| `or_all_sources_wide.csv` | 315 | 1,079 | 2.5 |
| `or_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 15 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 15 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 15 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 15 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 38 | 2022-01-01 | 2026-08-15 |
| Wastewater (NWSS) | influenza | 38 | 2022-01-01 | 2026-08-15 |
| Wastewater (NWSS) | rsv | 37 | 2022-09-03 | 2026-08-15 |

## Reliability flags

Number of rows in `or_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 604 | 64 | 0 | 46 | 19 | 209 |
| NHSN | hospital_reporting_count | 714 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 8,484 | 0 | 606 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 7,949 | 2,716 | 0 | 0 | 1,455 | 0 |
| NSSP | ed_visit_percent_smoothed | 8,376 | 477 | 0 | 1,004 | 2,263 | 0 |
| NSSP | participation_status | 2,222 | 0 | 606 | 0 | 0 | 0 |
| NWSS | participation_status | 15,765 | 0 | 2,282 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 18,003 | 0 | 0 | 44 | 0 | 0 |
| NWSS | wastewater_activity_level | 13,042 | 0 | 0 | 5,005 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for OR |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 37 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 38% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.76 |
| Wastewater: same, influenza A | 0.66 |
| Wastewater: same, RSV | 0.58 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `or_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `or_nssp_wide.csv` matches the long table | PASS | 36,158 cells; missing 0, unexpected 0, differing 0 |
| `or_nwss_wide.csv` matches the long table | PASS | 54,141 cells; missing 0, unexpected 0, differing 0 |
| `or_all_sources_wide.csv` matches the long table | PASS | 93,125 cells; missing 0, unexpected 0, differing 0 |
| `or_all_sources_wide.csv` census columns match `or_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 315 weeks, 2020-08-08 to 2026-08-15 |
