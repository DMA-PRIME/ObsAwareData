# New Hampshire (NH): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 33
- Emergency-department regions (CDC health service areas): 6
- Wastewater sampling sites: 20 (with COVID-19 data: 20; influenza A: 20; RSV: 20)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-12 (92 releases); ED visits 2025-08-15 to 2026-11-12 (53 releases); wastewater 2026-08-07 to 2026-11-13 (15 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nh_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `nh_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `nh_long_latest_2022.csv` | 2,938 | 15 | 0.6 |
| `nh_long_latest_2023.csv` | 7,868 | 15 | 1.8 |
| `nh_long_latest_2024.csv` | 11,051 | 15 | 2.5 |
| `nh_long_latest_2025.csv` | 11,750 | 15 | 2.6 |
| `nh_long_latest_2026.csv` | 10,656 | 15 | 2.4 |
| `nh_nhsn_wide.csv` | 327 | 24 | 0.1 |
| `nh_nssp_wide.csv` | 1,505 | 30 | 0.6 |
| `nh_nwss_wide.csv` | 3,282 | 24 | 0.9 |
| `nh_all_sources_wide.csv` | 327 | 569 | 1.3 |
| `nh_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-11-07 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-11-07 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-11-07 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | combined | 0 | none | none |
| Wastewater (NWSS) | covid | 20 | 2022-05-21 | 2026-11-07 |
| Wastewater (NWSS) | influenza | 20 | 2022-10-15 | 2026-11-07 |
| Wastewater (NWSS) | rsv | 20 | 2022-10-15 | 2026-11-07 |

## Reliability flags

Number of rows in `nh_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 699 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 578 | 139 | 0 | 36 | 19 | 209 |
| NHSN | hospital_reporting_count | 753 | 19 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 645 | 0 | 3,870 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 597 | 48 | 0 | 0 | 5,375 | 0 |
| NSSP | ed_visit_percent_smoothed | 541 | 37 | 0 | 67 | 5,375 | 0 |
| NSSP | participation_status | 1,290 | 0 | 0 | 0 | 0 | 0 |
| NWSS | participation_status | 6,662 | 0 | 1,382 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 6,662 | 0 | 0 | 1,382 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,662 | 0 | 0 | 1,382 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NH |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 20 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 118% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 46% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.92 |
| Wastewater: same, influenza A | 0.95 |
| Wastewater: same, RSV | 0.93 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`nh_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,566,851 rows covering 44,920 distinct values. Of those, 14,015 (31.2%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 126 | 2025-04-04 | 2026-11-13 | 332,154 |
| NSSP | 58 | 2025-08-15 | 2026-11-12 | 890,507 |
| NWSS | 15 | 2026-08-07 | 2026-11-13 | 344,190 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `nh_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nh_nhsn_wide.csv` matches the long table | PASS | 2,943 cells; missing 0, unexpected 0, differing 0 |
| `nh_nssp_wide.csv` matches the long table | PASS | 17,845 cells; missing 0, unexpected 0, differing 0 |
| `nh_nwss_wide.csv` matches the long table | PASS | 24,132 cells; missing 0, unexpected 0, differing 0 |
| `nh_all_sources_wide.csv` matches the long table | PASS | 44,920 cells; missing 0, unexpected 0, differing 0 |
| `nh_all_sources_wide.csv` census columns match `nh_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 327 weeks, 2020-08-08 to 2026-11-07 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
