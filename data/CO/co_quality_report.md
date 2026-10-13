# Colorado (CO): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 08
- Emergency-department regions (CDC health service areas): 17
- Wastewater sampling sites: 67 (with COVID-19 data: 67; influenza A: 25; RSV: 23)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-08-07, 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `co_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `co_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `co_long_latest_2022.csv` | 11,584 | 16 | 2.7 |
| `co_long_latest_2023.csv` | 21,908 | 16 | 5.3 |
| `co_long_latest_2024.csv` | 22,820 | 16 | 5.6 |
| `co_long_latest_2025.csv` | 22,085 | 16 | 5.4 |
| `co_long_latest_2026.csv` | 16,674 | 16 | 4.1 |
| `co_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `co_nssp_wide.csv` | 3,762 | 30 | 1.5 |
| `co_nwss_wide.csv` | 9,731 | 24 | 2.0 |
| `co_all_sources_wide.csv` | 321 | 1,163 | 2.7 |
| `co_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 9 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 9 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 9 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 9 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 67 | 2022-01-01 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 25 | 2022-05-21 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 23 | 2022-05-21 | 2026-09-26 |

## Reliability flags

Number of rows in `co_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 681 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 643 | 55 | 0 | 46 | 10 | 209 |
| NHSN | hospital_reporting_count | 744 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,643 | 0 | 5,643 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 5,686 | 902 | 0 | 0 | 8,460 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,721 | 193 | 0 | 674 | 8,460 | 0 |
| NSSP | participation_status | 836 | 0 | 2,717 | 0 | 0 | 0 |
| NWSS | participation_status | 13,666 | 0 | 2,302 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 15,090 | 0 | 0 | 878 | 0 | 0 |
| NWSS | wastewater_activity_level | 15,090 | 0 | 0 | 878 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for CO |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 60 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 36% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.40 |
| Wastewater: same, influenza A | 0.96 |
| Wastewater: same, RSV | 0.97 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`co_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,752,295 rows covering 95,728 distinct values. Of those, 23,319 (24.4%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 2,032,610 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 422,577 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `co_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `co_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `co_nssp_wide.csv` matches the long table | PASS | 44,935 cells; missing 0, unexpected 0, differing 0 |
| `co_nwss_wide.csv` matches the long table | PASS | 47,904 cells; missing 0, unexpected 0, differing 0 |
| `co_all_sources_wide.csv` matches the long table | PASS | 95,728 cells; missing 0, unexpected 0, differing 0 |
| `co_all_sources_wide.csv` census columns match `co_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
