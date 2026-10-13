# New Jersey (NJ): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 34
- Emergency-department regions (CDC health service areas): 9
- Wastewater sampling sites: 27 (with COVID-19 data: 27; influenza A: 27; RSV: 27)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nj_long_latest.csv` | 66,555 | 17 | 20.3 |
| `nj_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `nj_nssp_wide.csv` | 2,100 | 30 | 0.8 |
| `nj_nwss_wide.csv` | 4,539 | 24 | 1.4 |
| `nj_all_sources_wide.csv` | 322 | 767 | 1.8 |
| `nj_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-21 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 10 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 10 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 10 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 27 | 2022-05-14 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 27 | 2022-08-06 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 27 | 2022-08-06 | 2026-10-03 |

## Reliability flags

Number of rows in `nj_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 685 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 687 | 6 | 0 | 46 | 18 | 209 |
| NHSN | hospital_reporting_count | 739 | 18 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,300 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 5,866 | 539 | 0 | 0 | 1,995 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,621 | 94 | 0 | 690 | 1,995 | 0 |
| NSSP | participation_status | 1,890 | 0 | 0 | 0 | 0 | 0 |
| NWSS | participation_status | 10,243 | 0 | 2,646 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 11,220 | 0 | 0 | 1,669 | 0 | 0 |
| NWSS | wastewater_activity_level | 9,297 | 0 | 0 | 3,592 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NJ |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 78 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 88% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.99 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.99 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`nj_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,829,495 rows covering 66,555 distinct values. Of those, 18,575 (27.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,150,016 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 376,575 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nj_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `nj_nssp_wide.csv` matches the long table | PASS | 24,990 cells; missing 0, unexpected 0, differing 0 |
| `nj_nwss_wide.csv` matches the long table | PASS | 38,667 cells; missing 0, unexpected 0, differing 0 |
| `nj_all_sources_wide.csv` matches the long table | PASS | 66,555 cells; missing 0, unexpected 0, differing 0 |
| `nj_all_sources_wide.csv` census columns match `nj_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
