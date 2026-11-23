# Texas (TX): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 48
- Emergency-department regions (CDC health service areas): 61
- Wastewater sampling sites: 124 (with COVID-19 data: 124; influenza A: 81; RSV: 81)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-20 (85 releases); ED visits 2025-08-15 to 2026-11-18 (54 releases); wastewater 2026-08-07 to 2026-11-20 (16 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `tx_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `tx_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `tx_long_latest_2022.csv` | 19,351 | 15 | 4.6 |
| `tx_long_latest_2023.csv` | 54,311 | 15 | 13.3 |
| `tx_long_latest_2024.csv` | 58,148 | 15 | 14.1 |
| `tx_long_latest_2025.csv` | 60,737 | 15 | 14.7 |
| `tx_long_latest_2026.csv` | 55,448 | 15 | 13.4 |
| `tx_nhsn_wide.csv` | 328 | 24 | 0.1 |
| `tx_nssp_wide.csv` | 13,392 | 30 | 5.3 |
| `tx_nwss_wide.csv` | 13,820 | 24 | 3.2 |
| `tx_all_sources_wide.csv` | 328 | 3,245 | 6.8 |
| `tx_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-11-14 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-11-14 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-11-14 |
| Emergency department visits (NSSP) | covid | 57 | 2022-10-01 | 2026-11-14 |
| Emergency department visits (NSSP) | influenza | 57 | 2022-10-01 | 2026-11-14 |
| Emergency department visits (NSSP) | rsv | 57 | 2022-10-01 | 2026-11-14 |
| Emergency department visits (NSSP) | combined | 57 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 124 | 2022-01-01 | 2026-11-14 |
| Wastewater (NWSS) | influenza | 81 | 2022-03-05 | 2026-11-14 |
| Wastewater (NWSS) | rsv | 81 | 2022-03-05 | 2026-11-14 |

## Reliability flags

Number of rows in `tx_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 700 | 0 | 75 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 705 | 14 | 0 | 46 | 10 | 209 |
| NHSN | hospital_reporting_count | 765 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 34,558 | 0 | 5,618 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 34,664 | 8,257 | 0 | 0 | 10,647 | 0 |
| NSSP | ed_visit_percent_smoothed | 35,590 | 499 | 0 | 4,888 | 12,591 | 0 |
| NSSP | participation_status | 4,320 | 0 | 8,856 | 0 | 0 | 0 |
| NWSS | participation_status | 24,932 | 0 | 3,472 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 26,113 | 0 | 0 | 2,291 | 0 | 0 |
| NWSS | wastewater_activity_level | 26,103 | 10 | 0 | 2,291 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for TX |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 119 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 63% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.57 |
| Wastewater: same, influenza A | 0.25 |
| Wastewater: same, RSV | 0.25 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`tx_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 9,782,582 rows covering 248,652 distinct values. Of those, 84,806 (34.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 128 | 2025-04-04 | 2026-11-20 | 338,058 |
| NSSP | 59 | 2025-08-15 | 2026-11-18 | 8,132,135 |
| NWSS | 16 | 2026-08-07 | 2026-11-20 | 1,312,389 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `tx_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `tx_nhsn_wide.csv` matches the long table | PASS | 2,952 cells; missing 0, unexpected 0, differing 0 |
| `tx_nssp_wide.csv` matches the long table | PASS | 160,488 cells; missing 0, unexpected 0, differing 0 |
| `tx_nwss_wide.csv` matches the long table | PASS | 85,212 cells; missing 0, unexpected 0, differing 0 |
| `tx_all_sources_wide.csv` matches the long table | PASS | 248,652 cells; missing 0, unexpected 0, differing 0 |
| `tx_all_sources_wide.csv` census columns match `tx_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 328 weeks, 2020-08-08 to 2026-11-14 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
