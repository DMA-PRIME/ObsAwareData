# Minnesota (MN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 27
- Emergency-department regions (CDC health service areas): 26
- Wastewater sampling sites: 38 (with COVID-19 data: 38; influenza A: 25; RSV: 22)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mn_long_latest.csv` | 100,145 | 17 | 33.5 |
| `mn_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `mn_nssp_wide.csv` | 5,454 | 30 | 2.1 |
| `mn_nwss_wide.csv` | 6,964 | 24 | 1.4 |
| `mn_all_sources_wide.csv` | 316 | 1,199 | 2.7 |
| `mn_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-07 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 22 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 22 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 22 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 22 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 38 | 2022-04-16 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 25 | 2022-09-03 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 22 | 2022-09-03 | 2026-08-22 |

## Reliability flags

Number of rows in `mn_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 661 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 582 | 59 | 0 | 46 | 46 | 209 |
| NHSN | hospital_reporting_count | 687 | 46 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 10,735 | 0 | 5,627 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 9,668 | 5,974 | 0 | 0 | 6,174 | 0 |
| NSSP | ed_visit_percent_smoothed | 10,814 | 578 | 0 | 1,317 | 9,107 | 0 |
| NSSP | participation_status | 4,040 | 0 | 1,212 | 0 | 0 | 0 |
| NWSS | participation_status | 9,641 | 0 | 1,050 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 9,426 | 0 | 0 | 1,265 | 0 | 0 |
| NWSS | wastewater_activity_level | 7,423 | 0 | 0 | 3,268 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 52 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.70 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.98 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mn_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `mn_nssp_wide.csv` matches the long table | PASS | 65,246 cells; missing 0, unexpected 0, differing 0 |
| `mn_nwss_wide.csv` matches the long table | PASS | 32,073 cells; missing 0, unexpected 0, differing 0 |
| `mn_all_sources_wide.csv` matches the long table | PASS | 100,145 cells; missing 0, unexpected 0, differing 0 |
| `mn_all_sources_wide.csv` census columns match `mn_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
