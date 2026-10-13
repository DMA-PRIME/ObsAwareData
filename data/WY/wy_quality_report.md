# Wyoming (WY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 56
- Emergency-department regions (CDC health service areas): 13
- Wastewater sampling sites: 8 (with COVID-19 data: 8; influenza A: 5; RSV: 2)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `wy_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `wy_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `wy_long_latest_2022.csv` | 3,010 | 16 | 0.7 |
| `wy_long_latest_2023.csv` | 9,788 | 16 | 2.3 |
| `wy_long_latest_2024.csv` | 11,237 | 16 | 2.6 |
| `wy_long_latest_2025.csv` | 11,420 | 16 | 2.7 |
| `wy_long_latest_2026.csv` | 8,618 | 16 | 2.0 |
| `wy_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `wy_nssp_wide.csv` | 2,940 | 30 | 1.1 |
| `wy_nwss_wide.csv` | 1,271 | 24 | 0.3 |
| `wy_all_sources_wide.csv` | 322 | 467 | 1.2 |
| `wy_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 14 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 14 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 14 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 11 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 8 | 2022-07-16 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 5 | 2023-08-12 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 2 | 2023-11-18 | 2026-09-05 |

## Reliability flags

Number of rows in `wy_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 687 | 0 | 70 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 558 | 154 | 0 | 35 | 10 | 209 |
| NHSN | hospital_reporting_count | 747 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,250 | 0 | 3,570 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,733 | 5,232 | 0 | 0 | 1,795 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,449 | 190 | 0 | 755 | 5,366 | 0 |
| NSSP | participation_status | 2,520 | 0 | 210 | 0 | 0 | 0 |
| NWSS | participation_status | 1,337 | 0 | 917 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,838 | 0 | 0 | 416 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,838 | 0 | 0 | 416 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for WY |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 21 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 160% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.93 |
| Wastewater: same, influenza A | 0.97 |
| Wastewater: same, RSV | 0.75 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`wy_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,980,059 rows covering 44,730 distinct values. Of those, 17,051 (38.1%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,613,888 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 63,267 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `wy_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `wy_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `wy_nssp_wide.csv` matches the long table | PASS | 35,070 cells; missing 0, unexpected 0, differing 0 |
| `wy_nwss_wide.csv` matches the long table | PASS | 6,762 cells; missing 0, unexpected 0, differing 0 |
| `wy_all_sources_wide.csv` matches the long table | PASS | 44,730 cells; missing 0, unexpected 0, differing 0 |
| `wy_all_sources_wide.csv` census columns match `wy_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
