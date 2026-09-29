# Iowa (IA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 19
- Emergency-department regions (CDC health service areas): 34
- Wastewater sampling sites: 18 (with COVID-19 data: 18; influenza A: 14; RSV: 14)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ia_long_latest.csv` | 105,875 | 17 | 35.1 |
| `ia_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ia_nssp_wide.csv` | 7,070 | 30 | 2.7 |
| `ia_nwss_wide.csv` | 2,270 | 24 | 0.6 |
| `ia_all_sources_wide.csv` | 316 | 1,157 | 2.7 |
| `ia_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 35 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 35 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 35 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 35 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 18 | 2022-05-07 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 14 | 2022-12-17 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 14 | 2022-12-17 | 2026-08-22 |

## Reliability flags

Number of rows in `ia_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 614 | 69 | 0 | 39 | 11 | 209 |
| NHSN | hospital_reporting_count | 722 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 14,886 | 0 | 6,324 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 13,907 | 10,978 | 0 | 0 | 3,395 | 0 |
| NSSP | ed_visit_percent_smoothed | 16,071 | 557 | 0 | 1,890 | 9,762 | 0 |
| NSSP | participation_status | 5,252 | 0 | 1,616 | 0 | 0 | 0 |
| NWSS | participation_status | 5,462 | 0 | 675 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 5,747 | 0 | 0 | 390 | 0 | 0 |
| NWSS | wastewater_activity_level | 4,921 | 0 | 0 | 1,216 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 44 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 150% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 36% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.47 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.92 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ia_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ia_nssp_wide.csv` matches the long table | PASS | 84,638 cells; missing 0, unexpected 0, differing 0 |
| `ia_nwss_wide.csv` matches the long table | PASS | 18,411 cells; missing 0, unexpected 0, differing 0 |
| `ia_all_sources_wide.csv` matches the long table | PASS | 105,875 cells; missing 0, unexpected 0, differing 0 |
| `ia_all_sources_wide.csv` census columns match `ia_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
