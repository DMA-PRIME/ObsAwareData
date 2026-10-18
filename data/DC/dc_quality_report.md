# District of Columbia (DC): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 11
- Emergency-department regions (CDC health service areas): 1
- Wastewater sampling sites: 1 (with COVID-19 data: 1; influenza A: 1; RSV: 1)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-16 (98 releases); ED visits 2025-08-15 to 2026-10-14 (49 releases); wastewater 2026-08-07 to 2026-09-18 (7 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `dc_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `dc_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `dc_long_latest_2022.csv` | 892 | 15 | 0.2 |
| `dc_long_latest_2023.csv` | 1,862 | 15 | 0.4 |
| `dc_long_latest_2024.csv` | 2,132 | 15 | 0.5 |
| `dc_long_latest_2025.csv` | 2,087 | 15 | 0.5 |
| `dc_long_latest_2026.csv` | 1,645 | 15 | 0.4 |
| `dc_nhsn_wide.csv` | 323 | 24 | 0.1 |
| `dc_nssp_wide.csv` | 422 | 30 | 0.1 |
| `dc_nwss_wide.csv` | 219 | 24 | 0.1 |
| `dc_all_sources_wide.csv` | 323 | 107 | 0.3 |
| `dc_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-10 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-31 | 2026-10-10 |
| Emergency department visits (NSSP) | covid | 2 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 2 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 2 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 2 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 1 | 2022-05-28 | 2026-09-12 |
| Wastewater (NWSS) | influenza | 1 | 2023-11-18 | 2026-09-12 |
| Wastewater (NWSS) | rsv | 1 | 2023-11-18 | 2026-09-12 |

## Reliability flags

Number of rows in `dc_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 723 | 0 | 37 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 537 | 171 | 0 | 36 | 16 | 209 |
| NHSN | hospital_reporting_count | 744 | 16 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 1,266 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 1,450 | 26 | 0 | 0 | 212 | 0 |
| NSSP | ed_visit_percent_smoothed | 1,282 | 3 | 0 | 191 | 212 | 0 |
| NSSP | participation_status | 0 | 0 | 211 | 0 | 0 | 0 |
| NWSS | participation_status | 505 | 0 | 0 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 467 | 0 | 0 | 38 | 0 | 0 |
| NWSS | wastewater_activity_level | 467 | 0 | 0 | 38 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for DC |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 7 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 125% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 1.00 |
| Wastewater: same, influenza A | 1.00 |
| Wastewater: same, RSV | 1.00 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`dc_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 552,319 rows covering 9,275 distinct values. Of those, 2,900 (31.3%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 118 | 2025-04-04 | 2026-10-16 | 308,718 |
| NSSP | 54 | 2025-08-15 | 2026-10-14 | 227,125 |
| NWSS | 11 | 2026-08-07 | 2026-10-16 | 16,476 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `dc_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `dc_nhsn_wide.csv` matches the long table | PASS | 2,907 cells; missing 0, unexpected 0, differing 0 |
| `dc_nssp_wide.csv` matches the long table | PASS | 4,853 cells; missing 0, unexpected 0, differing 0 |
| `dc_nwss_wide.csv` matches the long table | PASS | 1,515 cells; missing 0, unexpected 0, differing 0 |
| `dc_all_sources_wide.csv` matches the long table | PASS | 9,275 cells; missing 0, unexpected 0, differing 0 |
| `dc_all_sources_wide.csv` census columns match `dc_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 323 weeks, 2020-08-08 to 2026-10-10 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
