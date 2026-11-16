# Mississippi (MS): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 28
- Emergency-department regions (CDC health service areas): 25
- Wastewater sampling sites: 6 (with COVID-19 data: 6; influenza A: 5; RSV: 5)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-13 (98 releases); ED visits 2025-08-15 to 2026-11-12 (53 releases); wastewater 2026-08-07 to 2026-11-13 (15 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ms_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ms_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ms_long_latest_2022.csv` | 4,888 | 15 | 1.2 |
| `ms_long_latest_2023.csv` | 16,931 | 15 | 4.1 |
| `ms_long_latest_2024.csv` | 17,519 | 15 | 4.3 |
| `ms_long_latest_2025.csv` | 18,167 | 15 | 4.4 |
| `ms_long_latest_2026.csv` | 15,681 | 15 | 3.8 |
| `ms_nhsn_wide.csv` | 327 | 24 | 0.1 |
| `ms_nssp_wide.csv` | 5,590 | 30 | 2.1 |
| `ms_nwss_wide.csv` | 555 | 24 | 0.1 |
| `ms_all_sources_wide.csv` | 327 | 761 | 1.9 |
| `ms_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-11-07 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-11-07 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-11-07 |
| Emergency department visits (NSSP) | covid | 26 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | influenza | 26 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | rsv | 26 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | combined | 26 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 6 | 2022-08-06 | 2026-11-07 |
| Wastewater (NWSS) | influenza | 5 | 2023-11-18 | 2026-11-07 |
| Wastewater (NWSS) | rsv | 5 | 2023-11-18 | 2026-11-07 |

## Reliability flags

Number of rows in `ms_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 698 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 692 | 24 | 0 | 46 | 10 | 209 |
| NHSN | hospital_reporting_count | 762 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 15,480 | 0 | 1,290 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 15,162 | 4,338 | 0 | 0 | 2,860 | 0 |
| NSSP | ed_visit_percent_smoothed | 16,171 | 98 | 0 | 1,941 | 4,150 | 0 |
| NSSP | participation_status | 1,720 | 0 | 3,655 | 0 | 0 | 0 |
| NWSS | participation_status | 1,042 | 0 | 303 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,301 | 0 | 0 | 44 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,301 | 0 | 0 | 44 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MS |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 70 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 87% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.64 |
| Wastewater: same, influenza A | 0.90 |
| Wastewater: same, RSV | 0.89 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ms_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,724,577 rows covering 73,843 distinct values. Of those, 25,025 (33.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 126 | 2025-04-04 | 2026-11-13 | 332,154 |
| NSSP | 58 | 2025-08-15 | 2026-11-12 | 3,336,719 |
| NWSS | 15 | 2026-08-07 | 2026-11-13 | 55,704 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ms_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ms_nhsn_wide.csv` matches the long table | PASS | 2,943 cells; missing 0, unexpected 0, differing 0 |
| `ms_nssp_wide.csv` matches the long table | PASS | 66,865 cells; missing 0, unexpected 0, differing 0 |
| `ms_nwss_wide.csv` matches the long table | PASS | 4,035 cells; missing 0, unexpected 0, differing 0 |
| `ms_all_sources_wide.csv` matches the long table | PASS | 73,843 cells; missing 0, unexpected 0, differing 0 |
| `ms_all_sources_wide.csv` census columns match `ms_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 327 weeks, 2020-08-08 to 2026-11-07 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
