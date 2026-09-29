# Colorado (CO): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 08
- Emergency-department regions (CDC health service areas): 17
- Wastewater sampling sites: 67 (with COVID-19 data: 67; influenza A: 25; RSV: 23)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `co_long_latest.csv` | 93,134 | 17 | 30.7 |
| `co_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `co_nssp_wide.csv` | 3,636 | 30 | 1.5 |
| `co_nwss_wide.csv` | 9,617 | 24 | 1.9 |
| `co_all_sources_wide.csv` | 316 | 1,163 | 2.6 |
| `co_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 9 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 9 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 9 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 9 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 67 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 25 | 2022-05-21 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 23 | 2022-05-21 | 2026-08-22 |

## Reliability flags

Number of rows in `co_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 629 | 53 | 0 | 41 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,454 | 0 | 5,454 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 5,553 | 846 | 0 | 0 | 8,145 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,560 | 183 | 0 | 656 | 8,145 | 0 |
| NSSP | participation_status | 808 | 0 | 2,626 | 0 | 0 | 0 |
| NWSS | participation_status | 13,649 | 0 | 1,977 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 15,619 | 0 | 0 | 7 | 0 | 0 |
| NWSS | wastewater_activity_level | 11,972 | 0 | 0 | 3,654 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for CO |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 60 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 36% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.40 |
| Wastewater: same, influenza A | 0.96 |
| Wastewater: same, RSV | 0.97 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `co_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `co_nssp_wide.csv` matches the long table | PASS | 43,430 cells; missing 0, unexpected 0, differing 0 |
| `co_nwss_wide.csv` matches the long table | PASS | 46,878 cells; missing 0, unexpected 0, differing 0 |
| `co_all_sources_wide.csv` matches the long table | PASS | 93,134 cells; missing 0, unexpected 0, differing 0 |
| `co_all_sources_wide.csv` census columns match `co_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
