# Hawaii (HI): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 15
- Emergency-department regions (CDC health service areas): 3
- Wastewater sampling sites: 11 (with COVID-19 data: 11; influenza A: 10; RSV: 10)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-09; ED visits 2026-10-07; wastewater 2026-09-18, 2026-10-09

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `hi_long_latest.csv` | 28,758 | 17 | 8.3 |
| `hi_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `hi_nssp_wide.csv` | 840 | 30 | 0.3 |
| `hi_nwss_wide.csv` | 2,202 | 24 | 0.6 |
| `hi_all_sources_wide.csv` | 322 | 323 | 0.8 |
| `hi_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 4 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 4 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 4 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 4 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 11 | 2022-05-07 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 10 | 2023-01-21 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 10 | 2023-05-13 | 2026-10-03 |

## Reliability flags

Number of rows in `hi_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 684 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 619 | 84 | 0 | 44 | 10 | 209 |
| NHSN | hospital_reporting_count | 747 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 2,520 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 2,703 | 237 | 0 | 0 | 420 | 0 |
| NSSP | ed_visit_percent_smoothed | 2,589 | 1 | 0 | 350 | 420 | 0 |
| NSSP | participation_status | 420 | 0 | 210 | 0 | 0 | 0 |
| NWSS | participation_status | 2,598 | 0 | 2,732 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 3,912 | 0 | 0 | 1,418 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,297 | 0 | 0 | 2,033 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for HI |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 15 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 132% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 25% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.89 |
| Wastewater: same, influenza A | 0.99 |
| Wastewater: same, RSV | 0.99 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`hi_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 912,320 rows covering 28,758 distinct values. Of those, 7,999 (27.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 454,208 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 155,208 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `hi_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `hi_nssp_wide.csv` matches the long table | PASS | 9,870 cells; missing 0, unexpected 0, differing 0 |
| `hi_nwss_wide.csv` matches the long table | PASS | 15,990 cells; missing 0, unexpected 0, differing 0 |
| `hi_all_sources_wide.csv` matches the long table | PASS | 28,758 cells; missing 0, unexpected 0, differing 0 |
| `hi_all_sources_wide.csv` census columns match `hi_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
