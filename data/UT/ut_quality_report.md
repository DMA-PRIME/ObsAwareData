# Utah (UT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 49
- Emergency-department regions (CDC health service areas): 10
- Wastewater sampling sites: 34 (with COVID-19 data: 34; influenza A: 33; RSV: 33)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-06 (80 releases); ED visits 2025-08-15 to 2026-11-04 (52 releases); wastewater 2026-08-07 to 2026-11-06 (14 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ut_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ut_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ut_long_latest_2022.csv` | 7,528 | 15 | 1.6 |
| `ut_long_latest_2023.csv` | 12,926 | 15 | 2.9 |
| `ut_long_latest_2024.csv` | 14,003 | 15 | 3.1 |
| `ut_long_latest_2025.csv` | 22,463 | 15 | 5.0 |
| `ut_long_latest_2026.csv` | 18,718 | 15 | 4.1 |
| `ut_nhsn_wide.csv` | 326 | 24 | 0.1 |
| `ut_nssp_wide.csv` | 2,354 | 30 | 0.9 |
| `ut_nwss_wide.csv` | 8,091 | 24 | 1.8 |
| `ut_all_sources_wide.csv` | 326 | 905 | 2.1 |
| `ut_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-31 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-31 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-05 | 2026-10-31 |
| Emergency department visits (NSSP) | covid | 10 | 2022-10-01 | 2026-10-31 |
| Emergency department visits (NSSP) | influenza | 10 | 2022-10-01 | 2026-10-31 |
| Emergency department visits (NSSP) | rsv | 10 | 2022-10-01 | 2026-10-31 |
| Emergency department visits (NSSP) | combined | 10 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 34 | 2022-01-01 | 2026-10-31 |
| Wastewater (NWSS) | influenza | 33 | 2022-09-24 | 2026-10-31 |
| Wastewater (NWSS) | rsv | 33 | 2022-09-24 | 2026-10-31 |

## Reliability flags

Number of rows in `ut_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 694 | 0 | 75 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 584 | 109 | 0 | 58 | 18 | 209 |
| NHSN | hospital_reporting_count | 751 | 18 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,333 | 0 | 1,729 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 5,333 | 2,137 | 0 | 0 | 1,946 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,443 | 187 | 0 | 665 | 3,121 | 0 |
| NSSP | participation_status | 1,070 | 0 | 1,070 | 0 | 0 | 0 |
| NWSS | participation_status | 12,071 | 0 | 3,038 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 13,767 | 0 | 0 | 1,342 | 0 | 0 |
| NWSS | wastewater_activity_level | 13,767 | 0 | 0 | 1,342 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for UT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 40 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.97 |
| Wastewater: same, influenza A | 0.95 |
| Wastewater: same, RSV | 0.95 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ut_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,311,153 rows covering 76,295 distinct values. Of those, 25,168 (33.0%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 124 | 2025-04-04 | 2026-11-06 | 326,268 |
| NSSP | 57 | 2025-08-15 | 2026-11-04 | 1,377,334 |
| NWSS | 14 | 2026-08-07 | 2026-11-06 | 607,551 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ut_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ut_nhsn_wide.csv` matches the long table | PASS | 2,934 cells; missing 0, unexpected 0, differing 0 |
| `ut_nssp_wide.csv` matches the long table | PASS | 28,034 cells; missing 0, unexpected 0, differing 0 |
| `ut_nwss_wide.csv` matches the long table | PASS | 45,327 cells; missing 0, unexpected 0, differing 0 |
| `ut_all_sources_wide.csv` matches the long table | PASS | 76,295 cells; missing 0, unexpected 0, differing 0 |
| `ut_all_sources_wide.csv` census columns match `ut_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 326 weeks, 2020-08-08 to 2026-10-31 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
