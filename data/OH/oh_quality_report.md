# Ohio (OH): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 39
- Emergency-department regions (CDC health service areas): 28
- Wastewater sampling sites: 76 (with COVID-19 data: 76; influenza A: 73; RSV: 68)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `oh_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `oh_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `oh_long_latest_2022.csv` | 15,976 | 16 | 3.8 |
| `oh_long_latest_2023.csv` | 32,486 | 16 | 8.0 |
| `oh_long_latest_2024.csv` | 44,168 | 16 | 10.6 |
| `oh_long_latest_2025.csv` | 47,573 | 16 | 11.4 |
| `oh_long_latest_2026.csv` | 33,836 | 16 | 8.1 |
| `oh_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `oh_nssp_wide.csv` | 6,090 | 30 | 2.5 |
| `oh_nwss_wide.csv` | 16,225 | 24 | 3.7 |
| `oh_all_sources_wide.csv` | 322 | 2,039 | 5.0 |
| `oh_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 76 | 2022-01-01 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 73 | 2022-12-17 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 68 | 2022-12-17 | 2026-10-03 |

## Reliability flags

Number of rows in `oh_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 683 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 683 | 16 | 0 | 47 | 11 | 209 |
| NHSN | hospital_reporting_count | 746 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 630 | 0 | 17,640 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 713 | 22 | 0 | 0 | 23,625 | 0 |
| NSSP | ed_visit_percent_smoothed | 644 | 11 | 0 | 80 | 23,625 | 0 |
| NSSP | participation_status | 5,250 | 0 | 630 | 0 | 0 | 0 |
| NWSS | participation_status | 28,269 | 0 | 4,707 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 30,180 | 0 | 0 | 2,796 | 0 | 0 |
| NWSS | wastewater_activity_level | 30,178 | 2 | 0 | 2,796 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for OH |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 151 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 36% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.76 |
| Wastewater: same, RSV | 0.37 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`oh_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,619,597 rows covering 174,696 distinct values. Of those, 21,832 (12.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 3,353,408 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 963,285 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `oh_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `oh_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `oh_nssp_wide.csv` matches the long table | PASS | 72,870 cells; missing 0, unexpected 0, differing 0 |
| `oh_nwss_wide.csv` matches the long table | PASS | 98,928 cells; missing 0, unexpected 0, differing 0 |
| `oh_all_sources_wide.csv` matches the long table | PASS | 174,696 cells; missing 0, unexpected 0, differing 0 |
| `oh_all_sources_wide.csv` census columns match `oh_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
