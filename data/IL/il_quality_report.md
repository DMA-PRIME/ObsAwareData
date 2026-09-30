# Illinois (IL): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 17
- Emergency-department regions (CDC health service areas): 35
- Wastewater sampling sites: 89 (with COVID-19 data: 89; influenza A: 87; RSV: 85)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `il_long_latest.csv` | 223,562 | 17 | 72.9 |
| `il_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `il_nssp_wide.csv` | 7,272 | 30 | 2.8 |
| `il_nwss_wide.csv` | 16,924 | 24 | 4.7 |
| `il_all_sources_wide.csv` | 316 | 2,471 | 6.1 |
| `il_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 34 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 34 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 34 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 34 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 89 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 87 | 2022-08-06 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 85 | 2022-08-06 | 2026-08-22 |

## Reliability flags

Number of rows in `il_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 662 | 0 | 71 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 665 | 15 | 0 | 43 | 10 | 209 |
| NHSN | hospital_reporting_count | 723 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 19,178 | 0 | 2,638 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 17,926 | 6,248 | 0 | 0 | 4,914 | 0 |
| NSSP | ed_visit_percent_smoothed | 19,767 | 664 | 0 | 2,329 | 6,328 | 0 |
| NSSP | participation_status | 3,636 | 0 | 3,434 | 0 | 0 | 0 |
| NWSS | participation_status | 38,230 | 0 | 6,328 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 43,743 | 0 | 0 | 815 | 0 | 0 |
| NWSS | wastewater_activity_level | 36,005 | 0 | 0 | 8,553 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IL |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 109 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 103% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.90 |
| Wastewater: same, influenza A | 0.89 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`il_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,239,675 rows covering 223,562 distinct values. Of those, 55,483 (24.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 3,452,310 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 530,325 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `il_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `il_nssp_wide.csv` matches the long table | PASS | 87,062 cells; missing 0, unexpected 0, differing 0 |
| `il_nwss_wide.csv` matches the long table | PASS | 133,674 cells; missing 0, unexpected 0, differing 0 |
| `il_all_sources_wide.csv` matches the long table | PASS | 223,562 cells; missing 0, unexpected 0, differing 0 |
| `il_all_sources_wide.csv` census columns match `il_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
