# Washington (WA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 53
- Emergency-department regions (CDC health service areas): 15
- Wastewater sampling sites: 32 (with COVID-19 data: 32; influenza A: 29; RSV: 29)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (96 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wa_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `wa_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `wa_long_latest_2022.csv` | 5,533 | 15 | 1.3 |
| `wa_long_latest_2023.csv` | 17,219 | 15 | 4.0 |
| `wa_long_latest_2024.csv` | 21,374 | 15 | 4.9 |
| `wa_long_latest_2025.csv` | 19,703 | 15 | 4.6 |
| `wa_long_latest_2026.csv` | 16,770 | 15 | 3.9 |
| `wa_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `wa_nssp_wide.csv` | 3,392 | 30 | 1.4 |
| `wa_nwss_wide.csv` | 5,932 | 24 | 1.4 |
| `wa_all_sources_wide.csv` | 324 | 965 | 2.3 |
| `wa_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 32 | 2022-01-01 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 29 | 2023-08-19 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 29 | 2023-08-19 | 2026-10-17 |

## Reliability flags

Number of rows in `wa_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 692 | 0 | 71 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 658 | 54 | 0 | 46 | 5 | 209 |
| NHSN | hospital_reporting_count | 758 | 5 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 636 | 0 | 9,540 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 733 | 8 | 0 | 0 | 12,827 | 0 |
| NSSP | ed_visit_percent_smoothed | 653 | 1 | 0 | 87 | 12,827 | 0 |
| NSSP | participation_status | 2,544 | 0 | 636 | 0 | 0 | 0 |
| NWSS | participation_status | 10,350 | 0 | 2,266 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 11,866 | 0 | 0 | 750 | 0 | 0 |
| NWSS | wastewater_activity_level | 11,866 | 0 | 0 | 750 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 92 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 80% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 31% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.92 |
| Wastewater: same, influenza A | 0.93 |
| Wastewater: same, RSV | 0.47 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`wa_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,678,987 rows covering 81,256 distinct values. Of those, 12,869 (15.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 1,926,617 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 437,820 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `wa_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wa_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `wa_nssp_wide.csv` matches the long table | PASS | 40,492 cells; missing 0, unexpected 0, differing 0 |
| `wa_nwss_wide.csv` matches the long table | PASS | 37,848 cells; missing 0, unexpected 0, differing 0 |
| `wa_all_sources_wide.csv` matches the long table | PASS | 81,256 cells; missing 0, unexpected 0, differing 0 |
| `wa_all_sources_wide.csv` census columns match `wa_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
