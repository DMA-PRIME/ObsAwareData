# Virginia (VA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 51
- Emergency-department regions (CDC health service areas): 23
- Wastewater sampling sites: 48 (with COVID-19 data: 48; influenza A: 37; RSV: 37)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-09-18, 2026-09-25, 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `va_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `va_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `va_long_latest_2022.csv` | 9,535 | 16 | 2.5 |
| `va_long_latest_2023.csv` | 26,621 | 16 | 7.3 |
| `va_long_latest_2024.csv` | 31,391 | 16 | 8.4 |
| `va_long_latest_2025.csv` | 25,754 | 16 | 7.1 |
| `va_long_latest_2026.csv` | 17,907 | 16 | 5.0 |
| `va_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `va_nssp_wide.csv` | 5,016 | 30 | 2.2 |
| `va_nwss_wide.csv` | 8,309 | 24 | 1.9 |
| `va_all_sources_wide.csv` | 321 | 1,349 | 3.1 |
| `va_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 20 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 20 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 20 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 20 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 48 | 2022-01-01 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 37 | 2022-12-17 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 37 | 2022-12-17 | 2026-09-26 |

## Reliability flags

Number of rows in `va_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 682 | 0 | 72 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 684 | 12 | 0 | 48 | 10 | 209 |
| NHSN | hospital_reporting_count | 744 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 12,331 | 0 | 2,717 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 12,799 | 1,841 | 0 | 0 | 5,424 | 0 |
| NSSP | ed_visit_percent_smoothed | 12,859 | 233 | 0 | 1,548 | 5,424 | 0 |
| NSSP | participation_status | 0 | 0 | 4,807 | 0 | 0 | 0 |
| NWSS | participation_status | 13,152 | 0 | 3,179 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 14,355 | 0 | 0 | 1,976 | 0 | 0 |
| NWSS | wastewater_activity_level | 14,355 | 0 | 0 | 1,976 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for VA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 72 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 75% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 34% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.32 |
| Wastewater: same, influenza A | 0.51 |
| Wastewater: same, RSV | 0.42 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`va_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,443,288 rows covering 111,865 distinct values. Of those, 29,673 (26.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 2,713,298 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 432,882 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `va_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `va_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `va_nssp_wide.csv` matches the long table | PASS | 59,983 cells; missing 0, unexpected 0, differing 0 |
| `va_nwss_wide.csv` matches the long table | PASS | 48,993 cells; missing 0, unexpected 0, differing 0 |
| `va_all_sources_wide.csv` matches the long table | PASS | 111,865 cells; missing 0, unexpected 0, differing 0 |
| `va_all_sources_wide.csv` census columns match `va_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
