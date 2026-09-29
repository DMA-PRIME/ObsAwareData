# Arkansas (AR): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 05
- Emergency-department regions (CDC health service areas): 22
- Wastewater sampling sites: 21 (with COVID-19 data: 21; influenza A: 7; RSV: 7)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ar_long_latest.csv` | 69,146 | 17 | 23.5 |
| `ar_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ar_nssp_wide.csv` | 4,646 | 30 | 2.0 |
| `ar_nwss_wide.csv` | 1,885 | 24 | 0.4 |
| `ar_all_sources_wide.csv` | 316 | 803 | 2.0 |
| `ar_census_context.csv` | 24 | 6 | 0.0 |

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
| Wastewater (NWSS) | covid | 21 | 2022-06-11 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 7 | 2023-04-29 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 7 | 2023-04-29 | 2026-08-22 |

## Reliability flags

Number of rows in `ar_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 648 | 22 | 0 | 53 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 13,332 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 710 | 1 | 0 | 0 | 17,873 | 0 |
| NSSP | ed_visit_percent_smoothed | 633 | 0 | 0 | 78 | 17,873 | 0 |
| NSSP | participation_status | 1,818 | 0 | 2,626 | 0 | 0 | 0 |
| NWSS | participation_status | 3,169 | 0 | 421 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 3,181 | 0 | 0 | 409 | 0 | 0 |
| NWSS | wastewater_activity_level | 2,582 | 0 | 0 | 1,008 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for AR |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 55 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.22 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.91 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ar_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ar_nssp_wide.csv` matches the long table | PASS | 55,550 cells; missing 0, unexpected 0, differing 0 |
| `ar_nwss_wide.csv` matches the long table | PASS | 10,770 cells; missing 0, unexpected 0, differing 0 |
| `ar_all_sources_wide.csv` matches the long table | PASS | 69,146 cells; missing 0, unexpected 0, differing 0 |
| `ar_all_sources_wide.csv` census columns match `ar_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
