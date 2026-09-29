# New York (NY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 36
- Emergency-department regions (CDC health service areas): 21
- Wastewater sampling sites: 173 (with COVID-19 data: 173; influenza A: 83; RSV: 83)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ny_long_latest.csv` | 172,289 | 17 | 56.1 |
| `ny_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ny_nssp_wide.csv` | 4,444 | 30 | 1.7 |
| `ny_nwss_wide.csv` | 31,480 | 24 | 5.5 |
| `ny_all_sources_wide.csv` | 316 | 2,603 | 5.0 |
| `ny_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 21 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 21 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 21 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 21 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 173 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 83 | 2023-08-05 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 83 | 2023-08-05 | 2026-08-22 |

## Reliability flags

Number of rows in `ny_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 661 | 27 | 0 | 45 | 0 | 209 |
| NHSN | hospital_reporting_count | 733 | 0 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 12,720 | 0 | 612 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 12,431 | 2,500 | 0 | 0 | 2,845 | 0 |
| NSSP | ed_visit_percent_smoothed | 12,859 | 541 | 0 | 1,531 | 2,845 | 0 |
| NSSP | participation_status | 3,434 | 0 | 808 | 0 | 0 | 0 |
| NWSS | participation_status | 33,412 | 0 | 5,367 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 37,572 | 0 | 0 | 1,207 | 0 | 0 |
| NWSS | wastewater_activity_level | 27,812 | 0 | 0 | 10,967 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NY |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 125 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 70% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.80 |
| Wastewater: same, influenza A | 0.77 |
| Wastewater: same, RSV | 0.68 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ny_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ny_nssp_wide.csv` matches the long table | PASS | 53,126 cells; missing 0, unexpected 0, differing 0 |
| `ny_nwss_wide.csv` matches the long table | PASS | 116,337 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` matches the long table | PASS | 172,289 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` census columns match `ny_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
