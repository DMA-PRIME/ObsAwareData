# Montana (MT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 30
- Emergency-department regions (CDC health service areas): 16
- Wastewater sampling sites: 9 (with COVID-19 data: 9; influenza A: 5; RSV: 5)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mt_long_latest.csv` | 49,325 | 17 | 17.0 |
| `mt_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `mt_nssp_wide.csv` | 3,434 | 30 | 1.4 |
| `mt_nwss_wide.csv` | 1,085 | 24 | 0.2 |
| `mt_all_sources_wide.csv` | 315 | 563 | 1.3 |
| `mt_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 15 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 15 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 15 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 15 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 9 | 2022-01-01 | 2026-08-15 |
| Wastewater (NWSS) | influenza | 5 | 2024-12-14 | 2026-06-27 |
| Wastewater (NWSS) | rsv | 5 | 2024-12-14 | 2026-06-27 |

## Reliability flags

Number of rows in `mt_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 661 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 525 | 154 | 0 | 44 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 7,272 | 0 | 3,030 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 6,332 | 4,333 | 0 | 0 | 3,071 | 0 |
| NSSP | ed_visit_percent_smoothed | 7,002 | 287 | 0 | 847 | 5,600 | 0 |
| NSSP | participation_status | 1,616 | 0 | 1,616 | 0 | 0 | 0 |
| NWSS | participation_status | 1,587 | 0 | 244 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,831 | 0 | 0 | 0 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,511 | 0 | 0 | 320 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 43 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.76 |
| Wastewater: same, influenza A | 0.87 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mt_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `mt_nssp_wide.csv` matches the long table | PASS | 41,006 cells; missing 0, unexpected 0, differing 0 |
| `mt_nwss_wide.csv` matches the long table | PASS | 5,493 cells; missing 0, unexpected 0, differing 0 |
| `mt_all_sources_wide.csv` matches the long table | PASS | 49,325 cells; missing 0, unexpected 0, differing 0 |
| `mt_all_sources_wide.csv` census columns match `mt_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 315 weeks, 2020-08-08 to 2026-08-15 |
