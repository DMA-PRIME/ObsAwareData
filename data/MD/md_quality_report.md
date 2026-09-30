# Maryland (MD): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 24
- Emergency-department regions (CDC health service areas): 9
- Wastewater sampling sites: 15 (with COVID-19 data: 15; influenza A: 11; RSV: 11)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `md_long_latest.csv` | 41,741 | 17 | 13.7 |
| `md_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `md_nssp_wide.csv` | 2,020 | 30 | 0.7 |
| `md_nwss_wide.csv` | 2,049 | 24 | 0.5 |
| `md_all_sources_wide.csv` | 316 | 503 | 1.1 |
| `md_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-14 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 10 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 10 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 10 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 10 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 15 | 2022-05-28 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 11 | 2022-12-17 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 11 | 2022-12-17 | 2026-08-22 |

## Reliability flags

Number of rows in `md_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 626 | 46 | 0 | 45 | 16 | 209 |
| NHSN | hospital_reporting_count | 717 | 16 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,060 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 6,085 | 1,025 | 0 | 0 | 970 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,968 | 78 | 0 | 862 | 1,172 | 0 |
| NSSP | participation_status | 1,616 | 0 | 202 | 0 | 0 | 0 |
| NWSS | participation_status | 4,354 | 0 | 605 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 4,540 | 0 | 0 | 419 | 0 | 0 |
| NWSS | wastewater_activity_level | 3,801 | 0 | 0 | 1,158 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MD |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 31 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.32 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.97 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`md_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,269,189 rows covering 41,741 distinct values. Of those, 11,806 (28.3%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 953,190 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 58,959 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `md_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `md_nssp_wide.csv` matches the long table | PASS | 24,038 cells; missing 0, unexpected 0, differing 0 |
| `md_nwss_wide.csv` matches the long table | PASS | 14,877 cells; missing 0, unexpected 0, differing 0 |
| `md_all_sources_wide.csv` matches the long table | PASS | 41,741 cells; missing 0, unexpected 0, differing 0 |
| `md_all_sources_wide.csv` census columns match `md_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
