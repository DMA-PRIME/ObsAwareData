# Washington (WA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 53
- Emergency-department regions (CDC health service areas): 15
- Wastewater sampling sites: 32 (with COVID-19 data: 32; influenza A: 29; RSV: 29)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-09 (96 releases); ED visits 2025-08-15 to 2026-10-07 (48 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wa_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `wa_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `wa_long_latest_2022.csv` | 5,533 | 15 | 1.3 |
| `wa_long_latest_2023.csv` | 17,219 | 15 | 4.0 |
| `wa_long_latest_2024.csv` | 21,374 | 15 | 4.9 |
| `wa_long_latest_2025.csv` | 19,703 | 15 | 4.6 |
| `wa_long_latest_2026.csv` | 15,902 | 15 | 3.7 |
| `wa_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `wa_nssp_wide.csv` | 3,360 | 30 | 1.4 |
| `wa_nwss_wide.csv` | 5,879 | 24 | 1.4 |
| `wa_all_sources_wide.csv` | 322 | 965 | 2.3 |
| `wa_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 32 | 2022-01-01 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 29 | 2023-08-19 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 29 | 2023-08-19 | 2026-10-03 |

## Reliability flags

Number of rows in `wa_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 686 | 0 | 71 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 653 | 54 | 0 | 45 | 5 | 209 |
| NHSN | hospital_reporting_count | 752 | 5 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 630 | 0 | 9,450 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 727 | 8 | 0 | 0 | 12,705 | 0 |
| NSSP | ed_visit_percent_smoothed | 649 | 1 | 0 | 85 | 12,705 | 0 |
| NSSP | participation_status | 2,520 | 0 | 630 | 0 | 0 | 0 |
| NWSS | participation_status | 10,300 | 0 | 2,160 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 11,790 | 0 | 0 | 670 | 0 | 0 |
| NWSS | wastewater_activity_level | 11,790 | 0 | 0 | 670 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,511,482 rows covering 80,388 distinct values. Of those, 11,953 (14.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,845,824 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 362,754 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `wa_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wa_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `wa_nssp_wide.csv` matches the long table | PASS | 40,110 cells; missing 0, unexpected 0, differing 0 |
| `wa_nwss_wide.csv` matches the long table | PASS | 37,380 cells; missing 0, unexpected 0, differing 0 |
| `wa_all_sources_wide.csv` matches the long table | PASS | 80,388 cells; missing 0, unexpected 0, differing 0 |
| `wa_all_sources_wide.csv` census columns match `wa_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
