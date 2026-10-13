# Vermont (VT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 50
- Emergency-department regions (CDC health service areas): 7
- Wastewater sampling sites: 11 (with COVID-19 data: 11; influenza A: 7; RSV: 7)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `vt_long_latest.csv` | 31,692 | 17 | 9.4 |
| `vt_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `vt_nssp_wide.csv` | 1,680 | 30 | 0.6 |
| `vt_nwss_wide.csv` | 1,226 | 24 | 0.3 |
| `vt_all_sources_wide.csv` | 322 | 383 | 0.9 |
| `vt_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 7 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 7 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 7 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 7 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 11 | 2022-05-07 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 7 | 2023-03-04 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 7 | 2023-03-04 | 2026-10-03 |

## Reliability flags

Number of rows in `vt_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 683 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 482 | 225 | 0 | 30 | 20 | 209 |
| NHSN | hospital_reporting_count | 737 | 20 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 4,410 | 0 | 630 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 3,760 | 1,385 | 0 | 0 | 1,575 | 0 |
| NSSP | ed_visit_percent_smoothed | 4,392 | 234 | 0 | 519 | 1,575 | 0 |
| NSSP | participation_status | 1,050 | 0 | 420 | 0 | 0 | 0 |
| NWSS | participation_status | 2,480 | 0 | 468 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 2,908 | 0 | 0 | 40 | 0 | 0 |
| NWSS | wastewater_activity_level | 2,412 | 0 | 0 | 536 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for VT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 8 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 109% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 44% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.28 |
| Wastewater: same, influenza A | 0.94 |
| Wastewater: same, RSV | 0.93 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`vt_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,307,570 rows covering 31,692 distinct values. Of those, 8,077 (25.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 918,080 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 86,586 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `vt_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `vt_nssp_wide.csv` matches the long table | PASS | 19,950 cells; missing 0, unexpected 0, differing 0 |
| `vt_nwss_wide.csv` matches the long table | PASS | 8,844 cells; missing 0, unexpected 0, differing 0 |
| `vt_all_sources_wide.csv` matches the long table | PASS | 31,692 cells; missing 0, unexpected 0, differing 0 |
| `vt_all_sources_wide.csv` census columns match `vt_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
