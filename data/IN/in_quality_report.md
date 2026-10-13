# Indiana (IN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 18
- Emergency-department regions (CDC health service areas): 29
- Wastewater sampling sites: 35 (with COVID-19 data: 35; influenza A: 30; RSV: 30)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `in_long_latest.csv` | 114,237 | 17 | 35.7 |
| `in_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `in_nssp_wide.csv` | 6,300 | 30 | 2.4 |
| `in_nwss_wide.csv` | 5,442 | 24 | 1.3 |
| `in_all_sources_wide.csv` | 322 | 1,331 | 3.1 |
| `in_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 29 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 29 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 29 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 29 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 35 | 2022-05-07 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 30 | 2022-08-20 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 30 | 2022-08-20 | 2026-10-03 |

## Reliability flags

Number of rows in `in_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 684 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 679 | 18 | 0 | 49 | 11 | 209 |
| NHSN | hospital_reporting_count | 746 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 15,540 | 0 | 3,360 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 15,015 | 6,300 | 0 | 0 | 3,885 | 0 |
| NSSP | ed_visit_percent_smoothed | 16,947 | 563 | 0 | 2,020 | 5,670 | 0 |
| NSSP | participation_status | 1,680 | 0 | 4,410 | 0 | 0 | 0 |
| NWSS | participation_status | 10,509 | 0 | 1,474 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 10,749 | 0 | 0 | 1,234 | 0 | 0 |
| NWSS | wastewater_activity_level | 8,895 | 0 | 0 | 3,088 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 100 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 87% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`in_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,121,042 rows covering 114,237 distinct values. Of those, 31,029 (27.2%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 3,469,376 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 348,762 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `in_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `in_nssp_wide.csv` matches the long table | PASS | 75,390 cells; missing 0, unexpected 0, differing 0 |
| `in_nwss_wide.csv` matches the long table | PASS | 35,949 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` matches the long table | PASS | 114,237 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` census columns match `in_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
