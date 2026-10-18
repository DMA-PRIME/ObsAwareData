# North Dakota (ND): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 38
- Emergency-department regions (CDC health service areas): 13
- Wastewater sampling sites: 2 (with COVID-19 data: 2; influenza A: 0; RSV: 0)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-16 (79 releases); ED visits 2025-08-15 to 2026-10-14 (49 releases); wastewater 2026-08-07 to 2026-08-14 (2 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nd_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `nd_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `nd_long_latest_2022.csv` | 2,908 | 15 | 0.7 |
| `nd_long_latest_2023.csv` | 9,356 | 15 | 2.3 |
| `nd_long_latest_2024.csv` | 9,152 | 15 | 2.3 |
| `nd_long_latest_2025.csv` | 9,152 | 15 | 2.3 |
| `nd_long_latest_2026.csv` | 7,216 | 15 | 1.8 |
| `nd_nhsn_wide.csv` | 323 | 24 | 0.1 |
| `nd_nssp_wide.csv` | 2,954 | 30 | 1.3 |
| `nd_nwss_wide.csv` | 99 | 12 | 0.0 |
| `nd_all_sources_wide.csv` | 323 | 389 | 1.1 |
| `nd_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-10 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-10 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 1 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 2 | 2022-08-27 | 2023-09-16 |
| Wastewater (NWSS) | influenza | 0 | none | none |
| Wastewater (NWSS) | rsv | 0 | none | none |

## Reliability flags

Number of rows in `nd_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 686 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 582 | 124 | 0 | 43 | 11 | 209 |
| NHSN | hospital_reporting_count | 749 | 11 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 633 | 0 | 8,229 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 687 | 51 | 0 | 0 | 11,078 | 0 |
| NSSP | ed_visit_percent_smoothed | 641 | 23 | 0 | 74 | 11,078 | 0 |
| NSSP | participation_status | 633 | 0 | 2,110 | 0 | 0 | 0 |
| NWSS | participation_status | 54 | 0 | 45 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 91 | 0 | 0 | 8 | 0 | 0 |
| NWSS | wastewater_activity_level | 91 | 0 | 0 | 8 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for ND |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 22 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 133% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 50% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.87 |
| Wastewater: same, influenza A | not applicable (no sites) |
| Wastewater: same, RSV | not applicable (no sites) |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`nd_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,961,110 rows covering 38,441 distinct values. Of those, 1,355 (3.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 118 | 2025-04-04 | 2026-10-16 | 308,718 |
| NSSP | 54 | 2025-08-15 | 2026-10-14 | 1,649,125 |
| NWSS | 11 | 2026-08-07 | 2026-10-16 | 3,267 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `nd_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nd_nhsn_wide.csv` matches the long table | PASS | 2,907 cells; missing 0, unexpected 0, differing 0 |
| `nd_nssp_wide.csv` matches the long table | PASS | 35,237 cells; missing 0, unexpected 0, differing 0 |
| `nd_nwss_wide.csv` matches the long table | PASS | 297 cells; missing 0, unexpected 0, differing 0 |
| `nd_all_sources_wide.csv` matches the long table | PASS | 38,441 cells; missing 0, unexpected 0, differing 0 |
| `nd_all_sources_wide.csv` census columns match `nd_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 323 weeks, 2020-08-08 to 2026-10-10 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
