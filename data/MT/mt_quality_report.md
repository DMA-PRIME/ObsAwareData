# Montana (MT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 30
- Emergency-department regions (CDC health service areas): 16
- Wastewater sampling sites: 9 (with COVID-19 data: 9; influenza A: 5; RSV: 5)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (96 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mt_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `mt_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `mt_long_latest_2022.csv` | 3,805 | 15 | 0.9 |
| `mt_long_latest_2023.csv` | 11,489 | 15 | 2.9 |
| `mt_long_latest_2024.csv` | 11,786 | 15 | 2.9 |
| `mt_long_latest_2025.csv` | 13,478 | 15 | 3.3 |
| `mt_long_latest_2026.csv` | 10,302 | 15 | 2.6 |
| `mt_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `mt_nssp_wide.csv` | 3,604 | 30 | 1.4 |
| `mt_nwss_wide.csv` | 1,109 | 24 | 0.2 |
| `mt_all_sources_wide.csv` | 324 | 563 | 1.4 |
| `mt_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 15 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 15 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 15 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 15 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 9 | 2022-01-01 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 5 | 2024-12-14 | 2026-06-27 |
| Wastewater (NWSS) | rsv | 5 | 2024-12-14 | 2026-06-27 |

## Reliability flags

Number of rows in `mt_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 691 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 540 | 163 | 0 | 50 | 10 | 209 |
| NHSN | hospital_reporting_count | 753 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,996 | 0 | 3,816 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 6,491 | 4,624 | 0 | 0 | 3,301 | 0 |
| NSSP | ed_visit_percent_smoothed | 7,091 | 315 | 0 | 848 | 6,162 | 0 |
| NSSP | participation_status | 1,696 | 0 | 1,696 | 0 | 0 | 0 |
| NWSS | participation_status | 1,013 | 0 | 842 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,757 | 0 | 0 | 98 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,757 | 0 | 0 | 98 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 43 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.76 |
| Wastewater: same, influenza A | 0.87 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`mt_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,428,460 rows covering 51,517 distinct values. Of those, 12,692 (24.6%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 2,047,661 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 66,249 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `mt_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mt_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `mt_nssp_wide.csv` matches the long table | PASS | 43,036 cells; missing 0, unexpected 0, differing 0 |
| `mt_nwss_wide.csv` matches the long table | PASS | 5,565 cells; missing 0, unexpected 0, differing 0 |
| `mt_all_sources_wide.csv` matches the long table | PASS | 51,517 cells; missing 0, unexpected 0, differing 0 |
| `mt_all_sources_wide.csv` census columns match `mt_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
