# New Mexico (NM): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 35
- Emergency-department regions (CDC health service areas): 13
- Wastewater sampling sites: 14 (with COVID-19 data: 14; influenza A: 2; RSV: 2)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nm_long_latest.csv` | 42,971 | 17 | 14.1 |
| `nm_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `nm_nssp_wide.csv` | 2,828 | 30 | 1.1 |
| `nm_nwss_wide.csv` | 1,625 | 24 | 0.3 |
| `nm_all_sources_wide.csv` | 316 | 485 | 1.1 |
| `nm_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 12 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 12 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 12 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 12 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 14 | 2022-05-07 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 2 | 2023-12-02 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 2 | 2023-12-02 | 2026-08-22 |

## Reliability flags

Number of rows in `nm_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 663 | 0 | 70 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 589 | 64 | 0 | 60 | 20 | 209 |
| NHSN | hospital_reporting_count | 713 | 20 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,666 | 0 | 1,818 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 6,444 | 2,088 | 0 | 0 | 2,780 | 0 |
| NSSP | ed_visit_percent_smoothed | 6,836 | 293 | 0 | 797 | 3,386 | 0 |
| NSSP | participation_status | 1,818 | 0 | 808 | 0 | 0 | 0 |
| NWSS | participation_status | 1,817 | 0 | 320 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 2,133 | 0 | 0 | 4 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,717 | 0 | 0 | 420 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NM |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 18 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.24 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.91 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nm_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `nm_nssp_wide.csv` matches the long table | PASS | 33,734 cells; missing 0, unexpected 0, differing 0 |
| `nm_nwss_wide.csv` matches the long table | PASS | 6,411 cells; missing 0, unexpected 0, differing 0 |
| `nm_all_sources_wide.csv` matches the long table | PASS | 42,971 cells; missing 0, unexpected 0, differing 0 |
| `nm_all_sources_wide.csv` census columns match `nm_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
