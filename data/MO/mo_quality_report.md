# Missouri (MO): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 29
- Emergency-department regions (CDC health service areas): 27
- Wastewater sampling sites: 80 (with COVID-19 data: 80; influenza A: 73; RSV: 65)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-14, 2026-08-21, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mo_long_latest.csv` | 142,018 | 17 | 47.2 |
| `mo_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `mo_nssp_wide.csv` | 5,656 | 30 | 2.2 |
| `mo_nwss_wide.csv` | 11,731 | 24 | 2.7 |
| `mo_all_sources_wide.csv` | 316 | 2,017 | 3.9 |
| `mo_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 28 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 28 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 28 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 0 | none | none |
| Wastewater (NWSS) | covid | 80 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 73 | 2022-09-03 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 65 | 2023-05-13 | 2026-08-22 |

## Reliability flags

Number of rows in `mo_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 647 | 25 | 0 | 51 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 15,423 | 0 | 1,545 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,951 | 12,017 | 0 | 0 | 5,656 | 0 |
| NSSP | ed_visit_percent_smoothed | 3,914 | 1,487 | 0 | 457 | 16,766 | 0 |
| NSSP | participation_status | 1,010 | 0 | 4,444 | 0 | 0 | 0 |
| NWSS | participation_status | 22,380 | 0 | 1,454 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 23,776 | 0 | 0 | 68 | 0 | 0 |
| NWSS | wastewater_activity_level | 18,438 | 0 | 0 | 5,406 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MO |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 66 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 50% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.34 |
| Wastewater: same, influenza A | 0.05 |
| Wastewater: same, RSV | 0.36 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`mo_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,135,093 rows covering 142,018 distinct values. Of those, 16,610 (11.7%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 9 | 2026-06-12 | 2026-08-14 | 596,300 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 281,753 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mo_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `mo_nssp_wide.csv` matches the long table | PASS | 67,670 cells; missing 0, unexpected 0, differing 0 |
| `mo_nwss_wide.csv` matches the long table | PASS | 71,522 cells; missing 0, unexpected 0, differing 0 |
| `mo_all_sources_wide.csv` matches the long table | PASS | 142,018 cells; missing 0, unexpected 0, differing 0 |
| `mo_all_sources_wide.csv` census columns match `mo_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
