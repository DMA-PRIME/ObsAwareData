# Michigan (MI): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 26
- Emergency-department regions (CDC health service areas): 25
- Wastewater sampling sites: 72 (with COVID-19 data: 63; influenza A: 55; RSV: 52)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mi_long_latest.csv` | 114,191 | 17 | 38.2 |
| `mi_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `mi_nssp_wide.csv` | 5,252 | 30 | 2.0 |
| `mi_nwss_wide.csv` | 9,844 | 24 | 2.0 |
| `mi_all_sources_wide.csv` | 316 | 1,685 | 3.2 |
| `mi_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 24 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 24 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 24 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 24 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 63 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 55 | 2022-04-23 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 52 | 2022-04-23 | 2026-08-22 |

## Reliability flags

Number of rows in `mi_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 661 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 654 | 36 | 0 | 43 | 0 | 209 |
| NHSN | hospital_reporting_count | 733 | 0 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 14,544 | 0 | 1,212 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 13,569 | 3,495 | 0 | 0 | 3,944 | 0 |
| NSSP | ed_visit_percent_smoothed | 14,058 | 858 | 0 | 1,744 | 4,348 | 0 |
| NSSP | participation_status | 3,232 | 0 | 1,818 | 0 | 0 | 0 |
| NWSS | participation_status | 14,811 | 0 | 1,370 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 15,048 | 0 | 0 | 1,133 | 0 | 0 |
| NWSS | wastewater_activity_level | 11,288 | 0 | 0 | 4,893 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MI |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 121 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.57 |
| Wastewater: same, influenza A | 0.19 |
| Wastewater: same, RSV | 0.33 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mi_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `mi_nssp_wide.csv` matches the long table | PASS | 62,822 cells; missing 0, unexpected 0, differing 0 |
| `mi_nwss_wide.csv` matches the long table | PASS | 48,543 cells; missing 0, unexpected 0, differing 0 |
| `mi_all_sources_wide.csv` matches the long table | PASS | 114,191 cells; missing 0, unexpected 0, differing 0 |
| `mi_all_sources_wide.csv` census columns match `mi_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
