# Oklahoma (OK): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 40
- Emergency-department regions (CDC health service areas): 26
- Wastewater sampling sites: 21 (with COVID-19 data: 21; influenza A: 18; RSV: 18)
- Source snapshot dates used for the latest values: hospital admissions 2026-08-14; ED visits 2026-08-14; wastewater 2026-08-07, 2026-08-14, 2026-08-21, 2026-08-28

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ok_long_latest.csv` | 92,131 | 17 | 30.8 |
| `ok_nhsn_wide.csv` | 314 | 24 | 0.1 |
| `ok_nssp_wide.csv` | 5,454 | 30 | 2.2 |
| `ok_nwss_wide.csv` | 3,155 | 24 | 0.8 |
| `ok_all_sources_wide.csv` | 316 | 1,021 | 2.6 |
| `ok_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-08-08 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-10 | 2026-08-08 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-08-08 |
| Emergency department visits (NSSP) | covid | 9 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | influenza | 9 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | rsv | 9 | 2022-10-01 | 2026-08-08 |
| Emergency department visits (NSSP) | combined | 9 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 21 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | influenza | 18 | 2022-01-01 | 2026-08-22 |
| Wastewater (NWSS) | rsv | 18 | 2022-08-20 | 2026-08-22 |

## Reliability flags

Number of rows in `ok_long_latest.csv` by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 660 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 644 | 30 | 0 | 50 | 9 | 209 |
| NHSN | hospital_reporting_count | 724 | 9 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,252 | 0 | 11,110 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,631 | 1,768 | 0 | 0 | 15,417 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,209 | 165 | 0 | 621 | 15,821 | 0 |
| NSSP | participation_status | 202 | 0 | 5,050 | 0 | 0 | 0 |
| NWSS | participation_status | 6,431 | 0 | 1,074 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 7,985 | 0 | 0 | 292 | 0 | 0 |
| NWSS | wastewater_activity_level | 6,618 | 0 | 0 | 1,659 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for OK |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 84 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.59 |
| Wastewater: same, influenza A | 0.57 |
| Wastewater: same, RSV | 0.50 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ok_long_all_versions.csv.gz`)

Location: a GitHub Release asset, not stored in the repository; see `metadata/release_assets.csv` for its download link and checksum.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,935,752 rows covering 92,131 distinct values. Of those, 10,681 (11.6%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 100 | 2025-04-04 | 2026-08-14 | 257,040 |
| NSSP | 45 | 2025-08-15 | 2026-08-14 | 2,587,230 |
| NWSS | 4 | 2026-08-07 | 2026-08-28 | 91,482 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ok_nhsn_wide.csv` matches the long table | PASS | 2,826 cells; missing 0, unexpected 0, differing 0 |
| `ok_nssp_wide.csv` matches the long table | PASS | 65,246 cells; missing 0, unexpected 0, differing 0 |
| `ok_nwss_wide.csv` matches the long table | PASS | 24,059 cells; missing 0, unexpected 0, differing 0 |
| `ok_all_sources_wide.csv` matches the long table | PASS | 92,131 cells; missing 0, unexpected 0, differing 0 |
| `ok_all_sources_wide.csv` census columns match `ok_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 316 weeks, 2020-08-08 to 2026-08-22 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
