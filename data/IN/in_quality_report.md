# Indiana (IN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 18
- Emergency-department regions (CDC health service areas): 29
- Wastewater sampling sites: 35 (with COVID-19 data: 35; influenza A: 30; RSV: 30)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-16 (93 releases); ED visits 2025-08-15 to 2026-10-14 (49 releases); wastewater 2026-08-07 to 2026-10-16 (11 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `in_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `in_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `in_long_latest_2022.csv` | 7,768 | 15 | 1.8 |
| `in_long_latest_2023.csv` | 24,056 | 15 | 5.8 |
| `in_long_latest_2024.csv` | 25,802 | 15 | 6.2 |
| `in_long_latest_2025.csv` | 31,688 | 15 | 7.4 |
| `in_long_latest_2026.csv` | 24,937 | 15 | 5.9 |
| `in_nhsn_wide.csv` | 323 | 24 | 0.1 |
| `in_nssp_wide.csv` | 6,330 | 30 | 2.5 |
| `in_nwss_wide.csv` | 5,476 | 24 | 1.3 |
| `in_all_sources_wide.csv` | 323 | 1,331 | 3.1 |
| `in_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-10 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-10 |
| Emergency department visits (NSSP) | covid | 29 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 29 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 29 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 29 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 35 | 2022-05-07 | 2026-10-10 |
| Wastewater (NWSS) | influenza | 30 | 2022-08-20 | 2026-10-10 |
| Wastewater (NWSS) | rsv | 30 | 2022-08-20 | 2026-10-10 |

## Reliability flags

Number of rows in `in_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 687 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 681 | 18 | 0 | 50 | 11 | 209 |
| NHSN | hospital_reporting_count | 749 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 15,613 | 0 | 3,376 | 0 | 1 | 0 |
| NSSP | ed_visit_percent | 15,064 | 6,338 | 0 | 0 | 3,918 | 0 |
| NSSP | ed_visit_percent_smoothed | 17,045 | 573 | 0 | 1,990 | 5,712 | 0 |
| NSSP | participation_status | 1,688 | 0 | 4,431 | 0 | 0 | 0 |
| NWSS | participation_status | 10,602 | 0 | 1,482 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 10,169 | 0 | 0 | 1,915 | 0 | 0 |
| NWSS | wastewater_activity_level | 10,169 | 0 | 0 | 1,915 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 100 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 87% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`in_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,238,857 rows covering 114,908 distinct values. Of those, 31,502 (27.4%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 118 | 2025-04-04 | 2026-10-16 | 308,718 |
| NSSP | 54 | 2025-08-15 | 2026-10-14 | 3,545,125 |
| NWSS | 11 | 2026-08-07 | 2026-10-16 | 385,014 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `in_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `in_nhsn_wide.csv` matches the long table | PASS | 2,907 cells; missing 0, unexpected 0, differing 0 |
| `in_nssp_wide.csv` matches the long table | PASS | 75,749 cells; missing 0, unexpected 0, differing 0 |
| `in_nwss_wide.csv` matches the long table | PASS | 36,252 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` matches the long table | PASS | 114,908 cells; missing 0, unexpected 0, differing 0 |
| `in_all_sources_wide.csv` census columns match `in_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 323 weeks, 2020-08-08 to 2026-10-10 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
