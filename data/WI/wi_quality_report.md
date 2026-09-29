# Wisconsin (WI): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 55
- Emergency-department regions (CDC health service areas): 25
- Wastewater sampling sites: 54 (with COVID-19 data: 54; influenza A: 28; RSV: 28)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wi_long_latest.csv` | 119,174 | 17 | 39.5 |
| `wi_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `wi_nssp_wide.csv` | 5,252 | 30 | 2.1 |
| `wi_nwss_wide.csv` | 10,092 | 24 | 2.2 |
| `wi_all_sources_wide.csv` | 316 | 1,325 | 3.3 |
| `wi_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-10 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 26 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 26 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 26 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 26 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 54 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 28 | 2022-08-06 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 28 | 2022-08-06 | 2026-08-22 |

## Reliability flags

Number of rows in `wi_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 635 | 43 | 0 | 40 | 15 | 209 |
| NHSN | hospital_reporting_count | 718 | 15 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 15,150 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 13,742 | 4,744 | 0 | 0 | 2,522 | 0 |
| NSSP | ed_visit_percent_smoothed | 14,885 | 816 | 0 | 1,775 | 3,532 | 0 |
| NSSP | participation_status | 3,434 | 0 | 1,616 | 0 | 0 | 0 |
| NWSS | participation_status | 17,132 | 0 | 710 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 16,881 | 0 | 0 | 961 | 0 | 0 |
| NWSS | wastewater_activity_level | 13,989 | 0 | 0 | 3,853 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WI |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 106 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 117% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.81 |
| Wastewater: same, influenza A | 0.72 |
| Wastewater: same, RSV | 0.35 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wi_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `wi_nssp_wide.csv` matches the long table | PASS | 62,822 cells; missing 0, unexpected 0, differing 0 |
| `wi_nwss_wide.csv` matches the long table | PASS | 53,526 cells; missing 0, unexpected 0, differing 0 |
| `wi_all_sources_wide.csv` matches the long table | PASS | 119,174 cells; missing 0, unexpected 0, differing 0 |
| `wi_all_sources_wide.csv` census columns match `wi_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
