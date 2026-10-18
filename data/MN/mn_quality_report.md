# Minnesota (MN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 27
- Emergency-department regions (CDC health service areas): 26
- Wastewater sampling sites: 39 (with COVID-19 data: 39; influenza A: 26; RSV: 23)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-16 (87 releases); ED visits 2025-08-15 to 2026-10-14 (49 releases); wastewater 2026-08-07 to 2026-10-16 (11 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mn_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `mn_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `mn_long_latest_2022.csv` | 9,016 | 15 | 2.1 |
| `mn_long_latest_2023.csv` | 23,318 | 15 | 5.6 |
| `mn_long_latest_2024.csv` | 23,519 | 15 | 5.6 |
| `mn_long_latest_2025.csv` | 25,610 | 15 | 6.1 |
| `mn_long_latest_2026.csv` | 22,573 | 15 | 5.3 |
| `mn_nhsn_wide.csv` | 323 | 24 | 0.1 |
| `mn_nssp_wide.csv` | 5,697 | 30 | 2.2 |
| `mn_nwss_wide.csv` | 7,158 | 24 | 1.4 |
| `mn_all_sources_wide.csv` | 323 | 1,217 | 2.8 |
| `mn_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-10 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-07 | 2026-10-10 |
| Emergency department visits (NSSP) | covid | 22 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 22 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 22 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 22 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 39 | 2022-04-16 | 2026-10-10 |
| Wastewater (NWSS) | influenza | 26 | 2022-09-03 | 2026-10-10 |
| Wastewater (NWSS) | rsv | 23 | 2022-09-03 | 2026-10-10 |

## Reliability flags

Number of rows in `mn_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 688 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 604 | 64 | 0 | 46 | 46 | 209 |
| NHSN | hospital_reporting_count | 714 | 46 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 12,046 | 0 | 5,045 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 9,918 | 6,318 | 0 | 0 | 6,552 | 0 |
| NSSP | ed_visit_percent_smoothed | 11,358 | 610 | 0 | 1,420 | 9,400 | 0 |
| NSSP | participation_status | 4,220 | 0 | 1,266 | 0 | 0 | 0 |
| NWSS | participation_status | 9,783 | 0 | 1,428 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 9,439 | 0 | 0 | 1,772 | 0 | 0 |
| NWSS | wastewater_activity_level | 9,439 | 0 | 0 | 1,772 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 52 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.70 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.98 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`mn_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,854,072 rows covering 104,693 distinct values. Of those, 29,057 (27.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 118 | 2025-04-04 | 2026-10-16 | 308,718 |
| NSSP | 54 | 2025-08-15 | 2026-10-14 | 3,189,625 |
| NWSS | 11 | 2026-08-07 | 2026-10-16 | 355,729 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `mn_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mn_nhsn_wide.csv` matches the long table | PASS | 2,907 cells; missing 0, unexpected 0, differing 0 |
| `mn_nssp_wide.csv` matches the long table | PASS | 68,153 cells; missing 0, unexpected 0, differing 0 |
| `mn_nwss_wide.csv` matches the long table | PASS | 33,633 cells; missing 0, unexpected 0, differing 0 |
| `mn_all_sources_wide.csv` matches the long table | PASS | 104,693 cells; missing 0, unexpected 0, differing 0 |
| `mn_all_sources_wide.csv` census columns match `mn_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 323 weeks, 2020-08-08 to 2026-10-10 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
