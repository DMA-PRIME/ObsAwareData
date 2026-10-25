# Florida (FL): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 12
- Emergency-department regions (CDC health service areas): 17
- Wastewater sampling sites: 27 (with COVID-19 data: 27; influenza A: 26; RSV: 26)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (83 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `fl_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `fl_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `fl_long_latest_2022.csv` | 6,010 | 15 | 1.4 |
| `fl_long_latest_2023.csv` | 18,275 | 15 | 4.5 |
| `fl_long_latest_2024.csv` | 20,462 | 15 | 4.9 |
| `fl_long_latest_2025.csv` | 20,315 | 15 | 4.9 |
| `fl_long_latest_2026.csv` | 13,962 | 15 | 3.4 |
| `fl_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `fl_nssp_wide.csv` | 3,816 | 30 | 1.6 |
| `fl_nwss_wide.csv` | 4,054 | 24 | 1.1 |
| `fl_all_sources_wide.csv` | 324 | 947 | 2.3 |
| `fl_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 27 | 2022-01-01 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 26 | 2022-04-09 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 26 | 2022-04-09 | 2026-10-17 |

## Reliability flags

Number of rows in `fl_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 689 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 697 | 9 | 0 | 47 | 10 | 209 |
| NHSN | hospital_reporting_count | 753 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 636 | 0 | 10,812 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 741 | 0 | 0 | 0 | 14,523 | 0 |
| NSSP | ed_visit_percent_smoothed | 647 | 0 | 0 | 94 | 14,523 | 0 |
| NSSP | participation_status | 2,968 | 0 | 636 | 0 | 0 | 0 |
| NWSS | participation_status | 9,096 | 0 | 1,299 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 6,679 | 0 | 0 | 3,716 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,679 | 0 | 0 | 3,716 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for FL |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 164 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 45% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 20% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.50 |
| Wastewater: same, influenza A | 0.47 |
| Wastewater: same, RSV | 0.34 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`fl_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,848,733 rows covering 79,681 distinct values. Of those, 12,371 (15.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 2,168,705 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 365,478 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `fl_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `fl_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `fl_nssp_wide.csv` matches the long table | PASS | 45,580 cells; missing 0, unexpected 0, differing 0 |
| `fl_nwss_wide.csv` matches the long table | PASS | 31,185 cells; missing 0, unexpected 0, differing 0 |
| `fl_all_sources_wide.csv` matches the long table | PASS | 79,681 cells; missing 0, unexpected 0, differing 0 |
| `fl_all_sources_wide.csv` census columns match `fl_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
