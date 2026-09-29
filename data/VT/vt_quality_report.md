# Vermont (VT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 50
- Emergency-department regions (CDC health service areas): 7
- Wastewater sampling sites: 11 (with COVID-19 data: 11; influenza A: 7; RSV: 7)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `vt_long_latest.csv` | 30,617 | 17 | 9.8 |
| `vt_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `vt_nssp_wide.csv` | 1,616 | 30 | 0.6 |
| `vt_nwss_wide.csv` | 1,199 | 24 | 0.3 |
| `vt_all_sources_wide.csv` | 316 | 383 | 0.8 |
| `vt_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 7 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 7 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 7 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 7 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 11 | 2022-05-07 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 7 | 2023-03-04 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 7 | 2023-03-04 | 2026-08-22 |

## Reliability flags

Number of rows in `vt_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 468 | 218 | 0 | 27 | 20 | 209 |
| NHSN | hospital_reporting_count | 713 | 20 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 4,242 | 0 | 606 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 3,687 | 1,290 | 0 | 0 | 1,487 | 0 |
| NSSP | ed_visit_percent_smoothed | 4,256 | 203 | 0 | 518 | 1,487 | 0 |
| NSSP | participation_status | 1,010 | 0 | 404 | 0 | 0 | 0 |
| NWSS | participation_status | 2,602 | 0 | 265 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 2,827 | 0 | 0 | 40 | 0 | 0 |
| NWSS | wastewater_activity_level | 2,307 | 0 | 0 | 560 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for VT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 8 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 109% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 44% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.28 |
| Wastewater: same, influenza A | 0.94 |
| Wastewater: same, RSV | 0.93 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `vt_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `vt_nssp_wide.csv` matches the long table | PASS | 19,190 cells; missing 0, unexpected 0, differing 0 |
| `vt_nwss_wide.csv` matches the long table | PASS | 8,601 cells; missing 0, unexpected 0, differing 0 |
| `vt_all_sources_wide.csv` matches the long table | PASS | 30,617 cells; missing 0, unexpected 0, differing 0 |
| `vt_all_sources_wide.csv` census columns match `vt_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
