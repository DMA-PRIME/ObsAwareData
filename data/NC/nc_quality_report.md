# North Carolina (NC): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 37
- Emergency-department regions (CDC health service areas): 32
- Wastewater sampling sites: 52 (with COVID-19 data: 52; influenza A: 38; RSV: 38)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nc_long_latest.csv` | 137,423 | 17 | 46.0 |
| `nc_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `nc_nssp_wide.csv` | 6,666 | 30 | 2.6 |
| `nc_nwss_wide.csv` | 9,163 | 24 | 2.2 |
| `nc_all_sources_wide.csv` | 316 | 1,601 | 3.7 |
| `nc_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 31 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 31 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 31 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 31 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 52 | 2022-01-08 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 38 | 2022-08-27 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 38 | 2022-08-27 | 2026-08-22 |

## Reliability flags

Number of rows in `nc_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 649 | 22 | 0 | 43 | 19 | 209 |
| NHSN | hospital_reporting_count | 714 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 18,382 | 0 | 1,616 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 19,102 | 2,939 | 0 | 0 | 4,623 | 0 |
| NSSP | ed_visit_percent_smoothed | 18,811 | 171 | 0 | 2,453 | 5,229 | 0 |
| NSSP | participation_status | 3,434 | 0 | 3,030 | 0 | 0 | 0 |
| NWSS | participation_status | 15,795 | 0 | 2,474 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 17,472 | 0 | 0 | 797 | 0 | 0 |
| NWSS | wastewater_activity_level | 14,795 | 0 | 0 | 3,474 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NC |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 91 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.37 |
| Wastewater: same, influenza A | 0.93 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nc_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `nc_nssp_wide.csv` matches the long table | PASS | 79,790 cells; missing 0, unexpected 0, differing 0 |
| `nc_nwss_wide.csv` matches the long table | PASS | 54,807 cells; missing 0, unexpected 0, differing 0 |
| `nc_all_sources_wide.csv` matches the long table | PASS | 137,423 cells; missing 0, unexpected 0, differing 0 |
| `nc_all_sources_wide.csv` census columns match `nc_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
