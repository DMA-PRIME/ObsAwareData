# Arizona (AZ): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 04
- Emergency-department regions (CDC health service areas): 6
- Wastewater sampling sites: 22 (with COVID-19 data: 22; influenza A: 21; RSV: 20)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `az_long_latest.csv` | 38,837 | 17 | 12.3 |
| `az_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `az_nssp_wide.csv` | 1,414 | 30 | 0.6 |
| `az_nwss_wide.csv` | 3,063 | 24 | 0.7 |
| `az_all_sources_wide.csv` | 316 | 587 | 1.2 |
| `az_census_context.csv` | 24 | 6 | 0.0 |

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
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 22 | 2022-01-08 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 21 | 2023-10-14 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 20 | 2023-10-14 | 2026-08-22 |

## Reliability flags

Number of rows in `az_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 660 | 15 | 0 | 50 | 8 | 209 |
| NHSN | hospital_reporting_count | 725 | 8 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 3,636 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 695 | 16 | 0 | 0 | 4,945 | 0 |
| NSSP | ed_visit_percent_smoothed | 621 | 14 | 0 | 76 | 4,945 | 0 |
| NSSP | participation_status | 1,010 | 0 | 202 | 0 | 0 | 0 |
| NWSS | participation_status | 4,950 | 0 | 1,465 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 6,411 | 0 | 0 | 4 | 0 | 0 |
| NWSS | wastewater_activity_level | 5,232 | 0 | 0 | 1,183 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for AZ |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 61 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 32% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.92 |
| Wastewater: same, influenza A | 0.94 |
| Wastewater: same, RSV | 0.08 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `az_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `az_nssp_wide.csv` matches the long table | PASS | 16,766 cells; missing 0, unexpected 0, differing 0 |
| `az_nwss_wide.csv` matches the long table | PASS | 19,245 cells; missing 0, unexpected 0, differing 0 |
| `az_all_sources_wide.csv` matches the long table | PASS | 38,837 cells; missing 0, unexpected 0, differing 0 |
| `az_all_sources_wide.csv` census columns match `az_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
