# Florida (FL): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 12
- Emergency-department regions (CDC health service areas): 17
- Wastewater sampling sites: 27 (with COVID-19 data: 27; influenza A: 26; RSV: 26)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `fl_long_latest.csv` | 76,514 | 17 | 26.0 |
| `fl_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `fl_nssp_wide.csv` | 3,636 | 30 | 1.6 |
| `fl_nwss_wide.csv` | 3,917 | 24 | 1.1 |
| `fl_all_sources_wide.csv` | 316 | 947 | 2.2 |
| `fl_census_context.csv` | 24 | 6 | 0.0 |

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
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 27 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 26 | 2022-04-09 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 26 | 2022-04-09 | 2026-08-22 |

## Reliability flags

Number of rows in `fl_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 670 | 9 | 0 | 44 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 10,302 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 711 | 0 | 0 | 0 | 13,833 | 0 |
| NSSP | ed_visit_percent_smoothed | 627 | 0 | 0 | 84 | 13,833 | 0 |
| NSSP | participation_status | 2,828 | 0 | 606 | 0 | 0 | 0 |
| NWSS | participation_status | 9,352 | 0 | 734 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 6,625 | 0 | 0 | 3,461 | 0 | 0 |
| NWSS | wastewater_activity_level | 5,597 | 0 | 0 | 4,489 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for FL |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 164 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 45% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 20% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.50 |
| Wastewater: same, influenza A | 0.47 |
| Wastewater: same, RSV | 0.34 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `fl_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `fl_nssp_wide.csv` matches the long table | PASS | 43,430 cells; missing 0, unexpected 0, differing 0 |
| `fl_nwss_wide.csv` matches the long table | PASS | 30,258 cells; missing 0, unexpected 0, differing 0 |
| `fl_all_sources_wide.csv` matches the long table | PASS | 76,514 cells; missing 0, unexpected 0, differing 0 |
| `fl_all_sources_wide.csv` census columns match `fl_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
