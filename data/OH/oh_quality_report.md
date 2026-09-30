# Ohio (OH): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 39
- Emergency-department regions (CDC health service areas): 28
- Wastewater sampling sites: 76 (with COVID-19 data: 76; influenza A: 73; RSV: 68)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `oh_long_latest.csv` | 168,839 | 17 | 55.3 |
| `oh_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `oh_nssp_wide.csv` | 5,858 | 30 | 2.4 |
| `oh_nwss_wide.csv` | 15,885 | 24 | 3.6 |
| `oh_all_sources_wide.csv` | 316 | 2,039 | 4.8 |
| `oh_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 76 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 73 | 2022-12-17 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 68 | 2022-12-17 | 2026-08-22 |

## Reliability flags

Number of rows in `oh_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 659 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 662 | 16 | 0 | 44 | 11 | 209 |
| NHSN | hospital_reporting_count | 722 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 606 | 0 | 16,968 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 690 | 21 | 0 | 0 | 22,721 | 0 |
| NSSP | ed_visit_percent_smoothed | 626 | 11 | 0 | 74 | 22,721 | 0 |
| NSSP | participation_status | 5,050 | 0 | 606 | 0 | 0 | 0 |
| NWSS | participation_status | 27,632 | 0 | 4,341 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 31,200 | 0 | 0 | 773 | 0 | 0 |
| NWSS | wastewater_activity_level | 25,882 | 2 | 0 | 6,089 | 0 | 0 |

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

## Revision history (`oh_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,413,724 rows covering 168,839 distinct values. Of those, 18,231 (10.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 2,779,470 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 377,214 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `oh_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `oh_nssp_wide.csv` matches the long table | PASS | 70,094 cells; missing 0, unexpected 0, differing 0 |
| `oh_nwss_wide.csv` matches the long table | PASS | 95,919 cells; missing 0, unexpected 0, differing 0 |
| `oh_all_sources_wide.csv` matches the long table | PASS | 168,839 cells; missing 0, unexpected 0, differing 0 |
| `oh_all_sources_wide.csv` census columns match `oh_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
