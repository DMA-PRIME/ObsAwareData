# Tennessee (TN): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 47
- Emergency-department regions (CDC health service areas): 28
- Wastewater sampling sites: 10 (with COVID-19 data: 10; influenza A: 4; RSV: 4)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `tn_long_latest.csv` | 78,305 | 17 | 26.8 |
| `tn_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `tn_nssp_wide.csv` | 5,858 | 30 | 2.3 |
| `tn_nwss_wide.csv` | 1,016 | 24 | 0.2 |
| `tn_all_sources_wide.csv` | 316 | 845 | 2.0 |
| `tn_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-29 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-28 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 29 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 29 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 29 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 29 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 10 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 4 | 2023-06-17 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 4 | 2023-06-17 | 2026-08-22 |

## Reliability flags

Number of rows in `tn_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 661 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 666 | 10 | 0 | 44 | 13 | 209 |
| NHSN | hospital_reporting_count | 720 | 13 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 16,956 | 0 | 618 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 16,726 | 3,893 | 0 | 0 | 2,813 | 0 |
| NSSP | ed_visit_percent_smoothed | 17,352 | 255 | 0 | 2,204 | 3,621 | 0 |
| NSSP | participation_status | 2,626 | 0 | 3,030 | 0 | 0 | 0 |
| NWSS | participation_status | 1,629 | 0 | 166 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,536 | 0 | 0 | 259 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,315 | 1 | 0 | 479 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for TN |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 62 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 80% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.27 |
| Wastewater: same, influenza A | 0.19 |
| Wastewater: same, RSV | 0.19 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`tn_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,057,864 rows covering 78,305 distinct values. Of those, 23,780 (30.4%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 2,779,470 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 21,354 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `tn_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `tn_nssp_wide.csv` matches the long table | PASS | 70,094 cells; missing 0, unexpected 0, differing 0 |
| `tn_nwss_wide.csv` matches the long table | PASS | 5,385 cells; missing 0, unexpected 0, differing 0 |
| `tn_all_sources_wide.csv` matches the long table | PASS | 78,305 cells; missing 0, unexpected 0, differing 0 |
| `tn_all_sources_wide.csv` census columns match `tn_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
