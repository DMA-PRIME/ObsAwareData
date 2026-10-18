# New York (NY): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 36
- Emergency-department regions (CDC health service areas): 21
- Wastewater sampling sites: 173 (with COVID-19 data: 173; influenza A: 84; RSV: 84)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-16 (86 releases); ED visits 2025-08-15 to 2026-10-14 (49 releases); wastewater 2026-08-07 to 2026-10-16 (11 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ny_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ny_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ny_long_latest_2022.csv` | 17,410 | 15 | 3.9 |
| `ny_long_latest_2023.csv` | 37,487 | 15 | 8.6 |
| `ny_long_latest_2024.csv` | 41,687 | 15 | 9.5 |
| `ny_long_latest_2025.csv` | 42,506 | 15 | 9.7 |
| `ny_long_latest_2026.csv` | 45,634 | 15 | 10.3 |
| `ny_nhsn_wide.csv` | 323 | 24 | 0.1 |
| `ny_nssp_wide.csv` | 4,642 | 30 | 1.8 |
| `ny_nwss_wide.csv` | 33,061 | 24 | 5.9 |
| `ny_all_sources_wide.csv` | 323 | 2,615 | 5.3 |
| `ny_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-10 |
| Emergency department visits (NSSP) | covid | 21 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 21 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 21 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 21 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 173 | 2022-01-01 | 2026-10-10 |
| Wastewater (NWSS) | influenza | 84 | 2023-08-05 | 2026-10-10 |
| Wastewater (NWSS) | rsv | 84 | 2023-08-05 | 2026-10-10 |

## Reliability flags

Number of rows in `ny_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 686 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 685 | 27 | 0 | 48 | 0 | 209 |
| NHSN | hospital_reporting_count | 760 | 0 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 13,078 | 0 | 848 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 12,822 | 2,676 | 0 | 0 | 3,070 | 0 |
| NSSP | ed_visit_percent_smoothed | 13,345 | 561 | 0 | 1,592 | 3,070 | 0 |
| NSSP | participation_status | 3,587 | 0 | 844 | 0 | 0 | 0 |
| NWSS | participation_status | 37,799 | 0 | 4,528 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 37,132 | 0 | 0 | 5,195 | 0 | 0 |
| NWSS | wastewater_activity_level | 37,132 | 0 | 0 | 5,195 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,175,149 rows covering 185,381 distinct values. Of those, 50,679 (27.3%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 118 | 2025-04-04 | 2026-10-16 | 308,718 |
| NSSP | 54 | 2025-08-15 | 2026-10-14 | 2,597,125 |
| NWSS | 11 | 2026-08-07 | 2026-10-16 | 1,269,306 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ny_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ny_nhsn_wide.csv` matches the long table | PASS | 2,907 cells; missing 0, unexpected 0, differing 0 |
| `ny_nssp_wide.csv` matches the long table | PASS | 55,493 cells; missing 0, unexpected 0, differing 0 |
| `ny_nwss_wide.csv` matches the long table | PASS | 126,981 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` matches the long table | PASS | 185,381 cells; missing 0, unexpected 0, differing 0 |
| `ny_all_sources_wide.csv` census columns match `ny_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 323 weeks, 2020-08-08 to 2026-10-10 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
