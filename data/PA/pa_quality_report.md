# Pennsylvania (PA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 42
- Emergency-department regions (CDC health service areas): 26
- Wastewater sampling sites: 49 (with COVID-19 data: 49; influenza A: 41; RSV: 34)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `pa_long_latest.csv` | 111,023 | 17 | 37.0 |
| `pa_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `pa_nssp_wide.csv` | 5,454 | 30 | 2.3 |
| `pa_nwss_wide.csv` | 7,721 | 24 | 1.7 |
| `pa_all_sources_wide.csv` | 316 | 1,433 | 3.2 |
| `pa_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 25 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 49 | 2022-02-05 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 41 | 2022-08-06 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 34 | 2022-08-06 | 2026-08-22 |

## Reliability flags

Number of rows in `pa_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 670 | 8 | 0 | 45 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 15,756 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 3,275 | 61 | 0 | 0 | 18,480 | 0 |
| NSSP | ed_visit_percent_smoothed | 2,982 | 15 | 0 | 339 | 18,480 | 0 |
| NSSP | participation_status | 3,636 | 0 | 1,616 | 0 | 0 | 0 |
| NWSS | participation_status | 12,431 | 0 | 1,886 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 13,917 | 0 | 0 | 400 | 0 | 0 |
| NWSS | wastewater_activity_level | 11,555 | 1 | 0 | 2,761 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for PA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 150 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 60% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 29% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.78 |
| Wastewater: same, RSV | 0.94 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `pa_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `pa_nssp_wide.csv` matches the long table | PASS | 65,246 cells; missing 0, unexpected 0, differing 0 |
| `pa_nwss_wide.csv` matches the long table | PASS | 42,951 cells; missing 0, unexpected 0, differing 0 |
| `pa_all_sources_wide.csv` matches the long table | PASS | 111,023 cells; missing 0, unexpected 0, differing 0 |
| `pa_all_sources_wide.csv` census columns match `pa_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
