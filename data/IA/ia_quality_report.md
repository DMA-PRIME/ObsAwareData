# Iowa (IA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 19
- Emergency-department regions (CDC health service areas): 34
- Wastewater sampling sites: 18 (with COVID-19 data: 18; influenza A: 14; RSV: 14)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ia_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `ia_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `ia_long_latest_2022.csv` | 6,826 | 16 | 1.7 |
| `ia_long_latest_2023.csv` | 25,169 | 16 | 6.2 |
| `ia_long_latest_2024.csv` | 27,443 | 16 | 6.8 |
| `ia_long_latest_2025.csv` | 28,241 | 16 | 6.9 |
| `ia_long_latest_2026.csv` | 21,620 | 16 | 5.3 |
| `ia_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ia_nssp_wide.csv` | 7,350 | 30 | 2.9 |
| `ia_nwss_wide.csv` | 2,343 | 24 | 0.6 |
| `ia_all_sources_wide.csv` | 322 | 1,157 | 3.0 |
| `ia_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 35 | 2022-10-01 | 2026-06-27 |
| Emergency department visits (NSSP) | influenza | 35 | 2022-10-01 | 2026-06-27 |
| Emergency department visits (NSSP) | rsv | 35 | 2022-10-01 | 2026-06-27 |
| Emergency department visits (NSSP) | combined | 35 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 18 | 2022-05-07 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 14 | 2022-12-17 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 14 | 2022-12-17 | 2026-10-03 |

## Reliability flags

Number of rows in `ia_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 684 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 631 | 72 | 0 | 43 | 11 | 209 |
| NHSN | hospital_reporting_count | 746 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 588 | 0 | 21,462 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 13,909 | 10,346 | 0 | 0 | 5,145 | 0 |
| NSSP | ed_visit_percent_smoothed | 15,614 | 263 | 0 | 1,805 | 11,718 | 0 |
| NSSP | participation_status | 5,460 | 0 | 1,680 | 0 | 0 | 0 |
| NWSS | participation_status | 5,669 | 0 | 687 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 5,733 | 0 | 0 | 623 | 0 | 0 |
| NWSS | wastewater_activity_level | 5,733 | 0 | 0 | 623 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,537,844 rows covering 109,956 distinct values. Of those, 38,078 (34.6%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 4,049,216 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 185,724 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ia_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ia_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ia_nssp_wide.csv` matches the long table | PASS | 87,990 cells; missing 0, unexpected 0, differing 0 |
| `ia_nwss_wide.csv` matches the long table | PASS | 19,068 cells; missing 0, unexpected 0, differing 0 |
| `ia_all_sources_wide.csv` matches the long table | PASS | 109,956 cells; missing 0, unexpected 0, differing 0 |
| `ia_all_sources_wide.csv` census columns match `ia_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
