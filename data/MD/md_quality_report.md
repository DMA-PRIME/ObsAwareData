# Maryland (MD): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 24
- Emergency-department regions (CDC health service areas): 9
- Wastewater sampling sites: 15 (with COVID-19 data: 15; influenza A: 11; RSV: 11)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `md_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `md_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `md_long_latest_2022.csv` | 3,079 | 16 | 0.7 |
| `md_long_latest_2023.csv` | 8,501 | 16 | 2.1 |
| `md_long_latest_2024.csv` | 10,796 | 16 | 2.6 |
| `md_long_latest_2025.csv` | 11,597 | 16 | 2.8 |
| `md_long_latest_2026.csv` | 8,313 | 16 | 2.0 |
| `md_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `md_nssp_wide.csv` | 2,090 | 30 | 0.8 |
| `md_nwss_wide.csv` | 2,083 | 24 | 0.5 |
| `md_all_sources_wide.csv` | 321 | 503 | 1.2 |
| `md_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-09-14 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 10 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 10 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 10 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 10 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 15 | 2022-05-28 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 11 | 2022-12-17 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 11 | 2022-12-17 | 2026-09-26 |

## Reliability flags

Number of rows in `md_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 680 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 641 | 48 | 0 | 49 | 16 | 209 |
| NHSN | hospital_reporting_count | 738 | 16 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,061 | 0 | 209 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 6,236 | 1,084 | 0 | 0 | 1,040 | 0 |
| NSSP | ed_visit_percent_smoothed | 6,132 | 61 | 0 | 918 | 1,249 | 0 |
| NSSP | participation_status | 1,672 | 0 | 209 | 0 | 0 | 0 |
| NWSS | participation_status | 3,792 | 0 | 1,269 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 4,442 | 0 | 0 | 619 | 0 | 0 |
| NWSS | wastewater_activity_level | 4,442 | 0 | 0 | 619 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MD |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 31 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.32 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.97 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`md_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,556,612 rows covering 42,943 distinct values. Of those, 12,971 (30.2%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 1,125,026 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 134,478 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `md_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `md_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `md_nssp_wide.csv` matches the long table | PASS | 24,871 cells; missing 0, unexpected 0, differing 0 |
| `md_nwss_wide.csv` matches the long table | PASS | 15,183 cells; missing 0, unexpected 0, differing 0 |
| `md_all_sources_wide.csv` matches the long table | PASS | 42,943 cells; missing 0, unexpected 0, differing 0 |
| `md_all_sources_wide.csv` census columns match `md_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
