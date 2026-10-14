# New York (NY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 36
- Emergency-department regions (CDC health service areas): 21
- Wastewater sampling sites: 173 (with COVID-19 data: 173; influenza A: 83; RSV: 83)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-09 (84 releases); ED visits 2025-08-15 to 2026-10-07 (48 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ny_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ny_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ny_long_latest_2022.csv` | 17,410 | 15 | 3.9 |
| `ny_long_latest_2023.csv` | 37,361 | 15 | 8.6 |
| `ny_long_latest_2024.csv` | 40,643 | 15 | 9.3 |
| `ny_long_latest_2025.csv` | 41,480 | 15 | 9.5 |
| `ny_long_latest_2026.csv` | 42,974 | 15 | 9.7 |
| `ny_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `ny_nssp_wide.csv` | 4,620 | 30 | 1.8 |
| `ny_nwss_wide.csv` | 32,423 | 24 | 5.7 |
| `ny_all_sources_wide.csv` | 322 | 2,603 | 5.2 |
| `ny_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 21 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 21 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 21 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 21 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 173 | 2022-01-01 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 83 | 2023-08-05 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 83 | 2023-08-05 | 2026-10-03 |

## Reliability flags

Number of rows in `ny_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 683 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 682 | 27 | 0 | 48 | 0 | 209 |
| NHSN | hospital_reporting_count | 757 | 0 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 13,016 | 0 | 844 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 12,775 | 2,660 | 0 | 0 | 3,045 | 0 |
| NSSP | ed_visit_percent_smoothed | 13,266 | 555 | 0 | 1,614 | 3,045 | 0 |
| NSSP | participation_status | 3,570 | 0 | 840 | 0 | 0 | 0 |
| NWSS | participation_status | 35,633 | 0 | 5,166 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 36,034 | 0 | 0 | 4,765 | 0 | 0 |
| NWSS | wastewater_activity_level | 36,034 | 0 | 0 | 4,765 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NY |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 125 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 70% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.80 |
| Wastewater: same, influenza A | 0.77 |
| Wastewater: same, RSV | 0.68 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ny_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,989,591 rows covering 180,525 distinct values. Of those, 46,317 (25.7%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 2,541,632 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 1,145,055 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ny_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ny_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `ny_nssp_wide.csv` matches the long table | PASS | 55,230 cells; missing 0, unexpected 0, differing 0 |
| `ny_nwss_wide.csv` matches the long table | PASS | 122,397 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` matches the long table | PASS | 180,525 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` census columns match `ny_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
