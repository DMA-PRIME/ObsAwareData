# Alabama (AL): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 01
- Emergency-department regions (CDC health service areas): 20
- Wastewater sampling sites: 22 (with COVID-19 data: 22; influenza A: 20; RSV: 20)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `al_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `al_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `al_long_latest_2022.csv` | 5,038 | 16 | 1.3 |
| `al_long_latest_2023.csv` | 16,187 | 16 | 4.1 |
| `al_long_latest_2024.csv` | 17,222 | 16 | 4.4 |
| `al_long_latest_2025.csv` | 21,575 | 16 | 5.4 |
| `al_long_latest_2026.csv` | 16,422 | 16 | 4.1 |
| `al_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `al_nssp_wide.csv` | 4,389 | 30 | 1.9 |
| `al_nwss_wide.csv` | 2,584 | 24 | 0.7 |
| `al_all_sources_wide.csv` | 321 | 917 | 2.2 |
| `al_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 22 | 2022-07-23 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 20 | 2022-08-13 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 20 | 2022-08-13 | 2026-09-26 |

## Reliability flags

Number of rows in `al_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 681 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 666 | 29 | 0 | 48 | 11 | 209 |
| NHSN | hospital_reporting_count | 743 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 627 | 0 | 12,540 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 731 | 1 | 0 | 0 | 16,824 | 0 |
| NSSP | ed_visit_percent_smoothed | 644 | 0 | 0 | 88 | 16,824 | 0 |
| NSSP | participation_status | 1,881 | 0 | 2,299 | 0 | 0 | 0 |
| NWSS | participation_status | 6,706 | 0 | 545 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 6,892 | 0 | 0 | 359 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,892 | 0 | 0 | 359 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for AL |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 59 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 30% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.85 |
| Wastewater: same, influenza A | 0.85 |
| Wastewater: same, RSV | 0.85 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`al_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,859,011 rows covering 77,101 distinct values. Of those, 7,762 (10.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 2,372,954 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 188,949 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `al_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `al_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `al_nssp_wide.csv` matches the long table | PASS | 52,459 cells; missing 0, unexpected 0, differing 0 |
| `al_nwss_wide.csv` matches the long table | PASS | 21,753 cells; missing 0, unexpected 0, differing 0 |
| `al_all_sources_wide.csv` matches the long table | PASS | 77,101 cells; missing 0, unexpected 0, differing 0 |
| `al_all_sources_wide.csv` census columns match `al_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
