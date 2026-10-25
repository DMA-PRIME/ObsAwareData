# Iowa (IA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 19
- Emergency-department regions (CDC health service areas): 34
- Wastewater sampling sites: 18 (with COVID-19 data: 18; influenza A: 14; RSV: 14)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-23 (92 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ia_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ia_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ia_long_latest_2022.csv` | 6,826 | 15 | 1.6 |
| `ia_long_latest_2023.csv` | 25,169 | 15 | 6.0 |
| `ia_long_latest_2024.csv` | 27,443 | 15 | 6.5 |
| `ia_long_latest_2025.csv` | 28,241 | 15 | 6.6 |
| `ia_long_latest_2026.csv` | 22,674 | 15 | 5.3 |
| `ia_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `ia_nssp_wide.csv` | 7,420 | 30 | 3.0 |
| `ia_nwss_wide.csv` | 2,365 | 24 | 0.7 |
| `ia_all_sources_wide.csv` | 324 | 1,157 | 3.0 |
| `ia_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 35 | 2022-10-01 | 2026-06-27 |
| Emergency department visits (NSSP) | influenza | 35 | 2022-10-01 | 2026-06-27 |
| Emergency department visits (NSSP) | rsv | 35 | 2022-10-01 | 2026-06-27 |
| Emergency department visits (NSSP) | combined | 35 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 18 | 2022-05-07 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 14 | 2022-12-17 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 14 | 2022-12-17 | 2026-10-17 |

## Reliability flags

Number of rows in `ia_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 690 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 636 | 72 | 0 | 44 | 11 | 209 |
| NHSN | hospital_reporting_count | 752 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 588 | 0 | 21,672 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 13,909 | 10,346 | 0 | 0 | 5,425 | 0 |
| NSSP | ed_visit_percent_smoothed | 15,529 | 242 | 0 | 1,715 | 12,194 | 0 |
| NSSP | participation_status | 5,512 | 0 | 1,696 | 0 | 0 | 0 |
| NWSS | participation_status | 5,841 | 0 | 581 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 5,792 | 0 | 0 | 630 | 0 | 0 |
| NWSS | wastewater_activity_level | 5,792 | 0 | 0 | 630 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 44 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 150% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 36% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.47 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.92 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ia_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,765,160 rows covering 111,010 distinct values. Of those, 38,561 (34.7%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 4,226,453 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 224,157 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ia_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ia_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `ia_nssp_wide.csv` matches the long table | PASS | 88,828 cells; missing 0, unexpected 0, differing 0 |
| `ia_nwss_wide.csv` matches the long table | PASS | 19,266 cells; missing 0, unexpected 0, differing 0 |
| `ia_all_sources_wide.csv` matches the long table | PASS | 111,010 cells; missing 0, unexpected 0, differing 0 |
| `ia_all_sources_wide.csv` census columns match `ia_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
