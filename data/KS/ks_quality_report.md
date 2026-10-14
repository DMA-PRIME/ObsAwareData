# Kansas (KS): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 20
- Emergency-department regions (CDC health service areas): 37
- Wastewater sampling sites: 15 (with COVID-19 data: 15; influenza A: 14; RSV: 14)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-09 (94 releases); ED visits 2025-08-15 to 2026-10-07 (48 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ks_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ks_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ks_long_latest_2022.csv` | 8,008 | 15 | 1.9 |
| `ks_long_latest_2023.csv` | 28,367 | 15 | 6.6 |
| `ks_long_latest_2024.csv` | 30,128 | 15 | 7.0 |
| `ks_long_latest_2025.csv` | 30,140 | 15 | 7.0 |
| `ks_long_latest_2026.csv` | 23,402 | 15 | 5.4 |
| `ks_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ks_nssp_wide.csv` | 7,980 | 30 | 3.0 |
| `ks_nwss_wide.csv` | 2,862 | 24 | 0.8 |
| `ks_all_sources_wide.csv` | 322 | 1,211 | 3.1 |
| `ks_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 37 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 37 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 37 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 37 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 15 | 2022-05-07 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 14 | 2022-08-06 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 14 | 2022-08-06 | 2026-10-03 |

## Reliability flags

Number of rows in `ks_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 681 | 0 | 76 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 630 | 55 | 0 | 62 | 10 | 209 |
| NHSN | hospital_reporting_count | 747 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 12,810 | 0 | 11,130 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 12,968 | 14,227 | 0 | 0 | 4,725 | 0 |
| NSSP | ed_visit_percent_smoothed | 14,339 | 459 | 0 | 1,687 | 15,435 | 0 |
| NSSP | participation_status | 5,460 | 0 | 2,310 | 0 | 0 | 0 |
| NWSS | participation_status | 6,568 | 0 | 850 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 6,190 | 0 | 0 | 1,228 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,190 | 0 | 0 | 1,228 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for KS |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 79 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.96 |
| Wastewater: same, influenza A | 0.97 |
| Wastewater: same, RSV | 0.97 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ks_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,916,538 rows covering 120,702 distinct values. Of those, 29,582 (24.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 4,397,120 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 216,514 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ks_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ks_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ks_nssp_wide.csv` matches the long table | PASS | 95,550 cells; missing 0, unexpected 0, differing 0 |
| `ks_nwss_wide.csv` matches the long table | PASS | 22,254 cells; missing 0, unexpected 0, differing 0 |
| `ks_all_sources_wide.csv` matches the long table | PASS | 120,702 cells; missing 0, unexpected 0, differing 0 |
| `ks_all_sources_wide.csv` census columns match `ks_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
