# Wisconsin (WI): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 55
- Emergency-department regions (CDC health service areas): 25
- Wastewater sampling sites: 54 (with COVID-19 data: 54; influenza A: 28; RSV: 28)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-08-07, 2026-09-04, 2026-09-18, 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wi_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `wi_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `wi_long_latest_2022.csv` | 13,003 | 16 | 3.1 |
| `wi_long_latest_2023.csv` | 26,879 | 16 | 6.6 |
| `wi_long_latest_2024.csv` | 29,840 | 16 | 7.3 |
| `wi_long_latest_2025.csv` | 29,888 | 16 | 7.3 |
| `wi_long_latest_2026.csv` | 21,522 | 16 | 5.3 |
| `wi_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `wi_nssp_wide.csv` | 5,434 | 30 | 2.2 |
| `wi_nwss_wide.csv` | 10,145 | 24 | 2.2 |
| `wi_all_sources_wide.csv` | 321 | 1,325 | 3.4 |
| `wi_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-10 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 26 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 26 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 26 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 26 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 54 | 2022-01-01 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 28 | 2022-08-06 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 28 | 2022-08-06 | 2026-09-26 |

## Reliability flags

Number of rows in `wi_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 678 | 0 | 76 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 648 | 46 | 0 | 45 | 15 | 209 |
| NHSN | hospital_reporting_count | 739 | 15 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 627 | 0 | 15,675 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 14,004 | 5,028 | 0 | 0 | 2,704 | 0 |
| NSSP | ed_visit_percent_smoothed | 15,232 | 889 | 0 | 1,866 | 3,749 | 0 |
| NSSP | participation_status | 3,553 | 0 | 1,672 | 0 | 0 | 0 |
| NWSS | participation_status | 17,257 | 0 | 710 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 15,943 | 0 | 0 | 2,024 | 0 | 0 |
| NWSS | wastewater_activity_level | 15,943 | 0 | 0 | 2,024 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WI |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 106 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 117% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.81 |
| Wastewater: same, influenza A | 0.72 |
| Wastewater: same, RSV | 0.35 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`wi_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,716,627 rows covering 121,789 distinct values. Of those, 25,829 (21.2%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 2,940,194 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 479,325 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `wi_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wi_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `wi_nssp_wide.csv` matches the long table | PASS | 64,999 cells; missing 0, unexpected 0, differing 0 |
| `wi_nwss_wide.csv` matches the long table | PASS | 53,901 cells; missing 0, unexpected 0, differing 0 |
| `wi_all_sources_wide.csv` matches the long table | PASS | 121,789 cells; missing 0, unexpected 0, differing 0 |
| `wi_all_sources_wide.csv` census columns match `wi_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
