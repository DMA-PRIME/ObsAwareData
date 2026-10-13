# Alaska (AK): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 02
- Emergency-department regions (CDC health service areas): 4
- Wastewater sampling sites: 5 (with COVID-19 data: 5; influenza A: 5; RSV: 5)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ak_long_latest.csv` | 21,669 | 17 | 8.3 |
| `ak_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ak_nssp_wide.csv` | 1,050 | 30 | 0.6 |
| `ak_nwss_wide.csv` | 855 | 24 | 0.2 |
| `ak_all_sources_wide.csv` | 322 | 251 | 0.6 |
| `ak_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 5 | 2022-06-04 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 5 | 2023-05-27 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 5 | 2023-05-27 | 2026-10-03 |

## Reliability flags

Number of rows in `ak_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 684 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 611 | 86 | 0 | 41 | 19 | 209 |
| NHSN | hospital_reporting_count | 738 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 630 | 0 | 2,520 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 711 | 24 | 0 | 0 | 3,465 | 0 |
| NSSP | ed_visit_percent_smoothed | 639 | 15 | 0 | 81 | 3,465 | 0 |
| NSSP | participation_status | 0 | 0 | 840 | 0 | 0 | 0 |
| NWSS | participation_status | 1,684 | 0 | 443 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,487 | 0 | 0 | 640 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,222 | 0 | 0 | 905 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for AK |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 17 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 149% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.80 |
| Wastewater: same, influenza A | 0.79 |
| Wastewater: same, RSV | 0.78 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ak_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 935,600 rows covering 21,669 distinct values. Of those, 3,265 (15.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 570,176 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 62,520 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ak_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ak_nssp_wide.csv` matches the long table | PASS | 12,390 cells; missing 0, unexpected 0, differing 0 |
| `ak_nwss_wide.csv` matches the long table | PASS | 6,381 cells; missing 0, unexpected 0, differing 0 |
| `ak_all_sources_wide.csv` matches the long table | PASS | 21,669 cells; missing 0, unexpected 0, differing 0 |
| `ak_all_sources_wide.csv` census columns match `ak_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
