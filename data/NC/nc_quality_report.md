# North Carolina (NC): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 37
- Emergency-department regions (CDC health service areas): 32
- Wastewater sampling sites: 53 (with COVID-19 data: 53; influenza A: 39; RSV: 39)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-16 (82 releases); ED visits 2025-08-15 to 2026-10-14 (49 releases); wastewater 2026-08-07 to 2026-10-16 (11 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nc_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `nc_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `nc_long_latest_2022.csv` | 11,617 | 15 | 2.7 |
| `nc_long_latest_2023.csv` | 30,041 | 15 | 7.2 |
| `nc_long_latest_2024.csv` | 35,186 | 15 | 8.3 |
| `nc_long_latest_2025.csv` | 37,385 | 15 | 8.8 |
| `nc_long_latest_2026.csv` | 29,794 | 15 | 7.0 |
| `nc_nhsn_wide.csv` | 323 | 24 | 0.1 |
| `nc_nssp_wide.csv` | 6,963 | 30 | 2.7 |
| `nc_nwss_wide.csv` | 9,664 | 24 | 2.3 |
| `nc_all_sources_wide.csv` | 323 | 1,619 | 3.9 |
| `nc_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-10 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-10 |
| Emergency department visits (NSSP) | covid | 31 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 31 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 31 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 31 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 53 | 2022-01-01 | 2026-10-10 |
| Wastewater (NWSS) | influenza | 39 | 2022-08-27 | 2026-10-10 |
| Wastewater (NWSS) | rsv | 39 | 2022-08-27 | 2026-10-10 |

## Reliability flags

Number of rows in `nc_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 686 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 673 | 22 | 0 | 46 | 19 | 209 |
| NHSN | hospital_reporting_count | 741 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 18,990 | 0 | 1,899 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 19,741 | 3,137 | 0 | 0 | 4,974 | 0 |
| NSSP | ed_visit_percent_smoothed | 19,522 | 147 | 0 | 2,576 | 5,607 | 0 |
| NSSP | participation_status | 3,587 | 0 | 3,165 | 0 | 0 | 0 |
| NWSS | participation_status | 16,599 | 0 | 2,877 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 17,944 | 0 | 0 | 1,532 | 0 | 0 |
| NWSS | wastewater_activity_level | 17,944 | 0 | 0 | 1,532 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NC |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 91 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.37 |
| Wastewater: same, influenza A | 0.93 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`nc_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,818,004 rows covering 144,680 distinct values. Of those, 50,519 (34.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 118 | 2025-04-04 | 2026-10-16 | 308,718 |
| NSSP | 54 | 2025-08-15 | 2026-10-14 | 3,900,625 |
| NWSS | 11 | 2026-08-07 | 2026-10-16 | 608,661 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `nc_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nc_nhsn_wide.csv` matches the long table | PASS | 2,907 cells; missing 0, unexpected 0, differing 0 |
| `nc_nssp_wide.csv` matches the long table | PASS | 83,345 cells; missing 0, unexpected 0, differing 0 |
| `nc_nwss_wide.csv` matches the long table | PASS | 58,428 cells; missing 0, unexpected 0, differing 0 |
| `nc_all_sources_wide.csv` matches the long table | PASS | 144,680 cells; missing 0, unexpected 0, differing 0 |
| `nc_all_sources_wide.csv` census columns match `nc_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 323 weeks, 2020-08-08 to 2026-10-10 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
