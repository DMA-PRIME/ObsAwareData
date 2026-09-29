# California (CA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 06
- Emergency-department regions (CDC health service areas): 30
- Wastewater sampling sites: 105 (with COVID-19 data: 105; influenza A: 99; RSV: 99)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ca_long_latest.csv` | 219,839 | 17 | 71.2 |
| `ca_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ca_nssp_wide.csv` | 6,262 | 30 | 2.6 |
| `ca_nwss_wide.csv` | 17,497 | 24 | 4.9 |
| `ca_all_sources_wide.csv` | 316 | 2,603 | 6.3 |
| `ca_census_context.csv` | 24 | 6 | 0.0 |

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
| Wastewater (NWSS) | covid | 105 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 99 | 2022-03-05 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 99 | 2022-03-05 | 2026-08-22 |

## Reliability flags

Number of rows in `ca_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 672 | 9 | 0 | 42 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 18,180 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 708 | 3 | 0 | 0 | 24,337 | 0 |
| NSSP | ed_visit_percent_smoothed | 632 | 3 | 0 | 76 | 24,337 | 0 |
| NSSP | participation_status | 3,838 | 0 | 2,222 | 0 | 0 | 0 |
| NWSS | participation_status | 42,287 | 0 | 5,070 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 41,718 | 0 | 0 | 5,639 | 0 | 0 |
| NWSS | wastewater_activity_level | 36,289 | 0 | 0 | 11,068 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for CA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 289 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 67% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 31% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.73 |
| Wastewater: same, influenza A | 0.83 |
| Wastewater: same, RSV | 0.78 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ca_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ca_nssp_wide.csv` matches the long table | PASS | 74,942 cells; missing 0, unexpected 0, differing 0 |
| `ca_nwss_wide.csv` matches the long table | PASS | 142,071 cells; missing 0, unexpected 0, differing 0 |
| `ca_all_sources_wide.csv` matches the long table | PASS | 219,839 cells; missing 0, unexpected 0, differing 0 |
| `ca_all_sources_wide.csv` census columns match `ca_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
