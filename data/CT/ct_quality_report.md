# Connecticut (CT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 09
- Emergency-department regions (CDC health service areas): 4
- Wastewater sampling sites: 17 (with COVID-19 data: 17; influenza A: 14; RSV: 14)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ct_long_latest.csv` | 30,123 | 17 | 9.0 |
| `ct_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ct_nssp_wide.csv` | 1,050 | 30 | 0.4 |
| `ct_nwss_wide.csv` | 2,542 | 24 | 0.6 |
| `ct_all_sources_wide.csv` | 322 | 431 | 0.9 |
| `ct_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-09-26 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 5 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 5 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 5 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 5 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 17 | 2022-05-07 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 14 | 2023-11-04 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 14 | 2023-10-28 | 2026-10-03 |

## Reliability flags

Number of rows in `ct_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 719 | 0 | 38 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 626 | 77 | 0 | 46 | 8 | 209 |
| NHSN | hospital_reporting_count | 749 | 8 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 3,150 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 3,423 | 252 | 0 | 0 | 525 | 0 |
| NSSP | ed_visit_percent_smoothed | 3,093 | 125 | 0 | 457 | 525 | 0 |
| NSSP | participation_status | 840 | 0 | 0 | 0 | 0 | 0 |
| NWSS | participation_status | 3,292 | 0 | 1,653 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 4,657 | 0 | 0 | 288 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,909 | 0 | 0 | 1,036 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for CT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 29 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 92% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.84 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.98 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ct_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,016,945 rows covering 30,123 distinct values. Of those, 7,658 (25.4%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 570,176 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 143,865 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ct_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ct_nssp_wide.csv` matches the long table | PASS | 12,390 cells; missing 0, unexpected 0, differing 0 |
| `ct_nwss_wide.csv` matches the long table | PASS | 14,835 cells; missing 0, unexpected 0, differing 0 |
| `ct_all_sources_wide.csv` matches the long table | PASS | 30,123 cells; missing 0, unexpected 0, differing 0 |
| `ct_all_sources_wide.csv` census columns match `ct_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
