# North Carolina (NC): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 37
- Emergency-department regions (CDC health service areas): 32
- Wastewater sampling sites: 53 (with COVID-19 data: 53; influenza A: 39; RSV: 39)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-30 (85 releases); ED visits 2025-08-15 to 2026-10-28 (51 releases); wastewater 2026-08-07 to 2026-10-30 (13 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nc_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `nc_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `nc_long_latest_2022.csv` | 11,617 | 15 | 2.7 |
| `nc_long_latest_2023.csv` | 30,041 | 15 | 7.2 |
| `nc_long_latest_2024.csv` | 35,186 | 15 | 8.3 |
| `nc_long_latest_2025.csv` | 37,385 | 15 | 8.8 |
| `nc_long_latest_2026.csv` | 31,196 | 15 | 7.4 |
| `nc_nhsn_wide.csv` | 325 | 24 | 0.1 |
| `nc_nssp_wide.csv` | 7,029 | 30 | 2.7 |
| `nc_nwss_wide.csv` | 9,730 | 24 | 2.3 |
| `nc_all_sources_wide.csv` | 325 | 1,619 | 3.9 |
| `nc_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-24 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-24 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-24 |
| Emergency department visits (NSSP) | covid | 31 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | influenza | 31 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | rsv | 31 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | combined | 31 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 53 | 2022-01-01 | 2026-10-24 |
| Wastewater (NWSS) | influenza | 39 | 2022-08-27 | 2026-10-24 |
| Wastewater (NWSS) | rsv | 39 | 2022-08-27 | 2026-10-24 |

## Reliability flags

Number of rows in `nc_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 692 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 679 | 22 | 0 | 46 | 19 | 209 |
| NHSN | hospital_reporting_count | 747 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 19,170 | 0 | 1,917 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 19,898 | 3,166 | 0 | 0 | 5,052 | 0 |
| NSSP | ed_visit_percent_smoothed | 19,674 | 146 | 0 | 2,605 | 5,691 | 0 |
| NSSP | participation_status | 3,621 | 0 | 3,195 | 0 | 0 | 0 |
| NWSS | participation_status | 16,536 | 0 | 3,138 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 18,136 | 0 | 0 | 1,538 | 0 | 0 |
| NWSS | wastewater_activity_level | 18,136 | 0 | 0 | 1,538 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 5,112,131 rows covering 146,082 distinct values. Of those, 51,334 (35.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 122 | 2025-04-04 | 2026-10-30 | 320,400 |
| NSSP | 56 | 2025-08-15 | 2026-10-28 | 4,068,500 |
| NWSS | 13 | 2026-08-07 | 2026-10-30 | 723,231 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `nc_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nc_nhsn_wide.csv` matches the long table | PASS | 2,925 cells; missing 0, unexpected 0, differing 0 |
| `nc_nssp_wide.csv` matches the long table | PASS | 84,135 cells; missing 0, unexpected 0, differing 0 |
| `nc_nwss_wide.csv` matches the long table | PASS | 59,022 cells; missing 0, unexpected 0, differing 0 |
| `nc_all_sources_wide.csv` matches the long table | PASS | 146,082 cells; missing 0, unexpected 0, differing 0 |
| `nc_all_sources_wide.csv` census columns match `nc_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 325 weeks, 2020-08-08 to 2026-10-24 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
