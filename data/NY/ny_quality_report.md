# New York (NY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 36
- Emergency-department regions (CDC health service areas): 21
- Wastewater sampling sites: 173 (with COVID-19 data: 173; influenza A: 86; RSV: 86)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-13 (93 releases); ED visits 2025-08-15 to 2026-11-12 (53 releases); wastewater 2026-08-07 to 2026-11-13 (15 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ny_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ny_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ny_long_latest_2022.csv` | 17,719 | 15 | 4.0 |
| `ny_long_latest_2023.csv` | 37,754 | 15 | 8.7 |
| `ny_long_latest_2024.csv` | 41,921 | 15 | 9.6 |
| `ny_long_latest_2025.csv` | 42,989 | 15 | 9.8 |
| `ny_long_latest_2026.csv` | 50,367 | 15 | 11.4 |
| `ny_nhsn_wide.csv` | 327 | 24 | 0.1 |
| `ny_nssp_wide.csv` | 4,730 | 30 | 1.8 |
| `ny_nwss_wide.csv` | 33,947 | 24 | 6.1 |
| `ny_all_sources_wide.csv` | 327 | 2,639 | 5.4 |
| `ny_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-11-07 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-11-07 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-11-07 |
| Emergency department visits (NSSP) | covid | 21 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | influenza | 21 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | rsv | 21 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | combined | 21 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 173 | 2022-01-01 | 2026-11-07 |
| Wastewater (NWSS) | influenza | 86 | 2023-08-05 | 2026-11-07 |
| Wastewater (NWSS) | rsv | 86 | 2023-08-05 | 2026-11-07 |

## Reliability flags

Number of rows in `ny_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 698 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 696 | 27 | 0 | 49 | 0 | 209 |
| NHSN | hospital_reporting_count | 772 | 0 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 13,326 | 0 | 864 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 13,026 | 2,724 | 0 | 0 | 3,170 | 0 |
| NSSP | ed_visit_percent_smoothed | 13,558 | 544 | 0 | 1,648 | 3,170 | 0 |
| NSSP | participation_status | 3,655 | 0 | 860 | 0 | 0 | 0 |
| NWSS | participation_status | 38,479 | 0 | 5,494 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 38,628 | 0 | 0 | 5,345 | 0 | 0 |
| NWSS | wastewater_activity_level | 38,628 | 0 | 0 | 5,345 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NY |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 125 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 70% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.80 |
| Wastewater: same, influenza A | 0.77 |
| Wastewater: same, RSV | 0.68 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ny_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,927,094 rows covering 191,407 distinct values. Of those, 52,481 (27.4%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 126 | 2025-04-04 | 2026-11-13 | 332,154 |
| NSSP | 58 | 2025-08-15 | 2026-11-12 | 2,821,727 |
| NWSS | 15 | 2026-08-07 | 2026-11-13 | 1,773,213 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ny_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ny_nhsn_wide.csv` matches the long table | PASS | 2,943 cells; missing 0, unexpected 0, differing 0 |
| `ny_nssp_wide.csv` matches the long table | PASS | 56,545 cells; missing 0, unexpected 0, differing 0 |
| `ny_nwss_wide.csv` matches the long table | PASS | 131,919 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` matches the long table | PASS | 191,407 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` census columns match `ny_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 327 weeks, 2020-08-08 to 2026-11-07 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
