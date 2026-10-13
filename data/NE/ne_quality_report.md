# Nebraska (NE): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 31
- Emergency-department regions (CDC health service areas): 25
- Wastewater sampling sites: 21 (with COVID-19 data: 21; influenza A: 18; RSV: 18)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ne_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `ne_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `ne_long_latest_2022.csv` | 6,856 | 16 | 1.7 |
| `ne_long_latest_2023.csv` | 20,762 | 16 | 5.2 |
| `ne_long_latest_2024.csv` | 23,786 | 16 | 5.9 |
| `ne_long_latest_2025.csv` | 24,155 | 16 | 6.0 |
| `ne_long_latest_2026.csv` | 18,264 | 16 | 4.5 |
| `ne_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `ne_nssp_wide.csv` | 5,434 | 30 | 2.2 |
| `ne_nwss_wide.csv` | 3,759 | 24 | 1.0 |
| `ne_all_sources_wide.csv` | 321 | 1,007 | 2.6 |
| `ne_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-09-26 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 23 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 23 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 23 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 23 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 21 | 2022-01-01 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 18 | 2023-08-05 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 18 | 2023-08-05 | 2026-09-26 |

## Reliability flags

Number of rows in `ne_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 680 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 619 | 86 | 0 | 40 | 9 | 209 |
| NHSN | hospital_reporting_count | 745 | 9 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,360 | 0 | 9,942 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 7,206 | 9,630 | 0 | 0 | 4,900 | 0 |
| NSSP | ed_visit_percent_smoothed | 7,682 | 413 | 0 | 1,216 | 12,425 | 0 |
| NSSP | participation_status | 1,254 | 0 | 3,971 | 0 | 0 | 0 |
| NWSS | participation_status | 7,401 | 0 | 1,463 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 7,489 | 0 | 0 | 1,375 | 0 | 0 |
| NWSS | wastewater_activity_level | 7,489 | 0 | 0 | 1,375 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NE |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 77 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 107% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.74 |
| Wastewater: same, influenza A | 0.96 |
| Wastewater: same, RSV | 0.94 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ne_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,471,020 rows covering 94,480 distinct values. Of those, 18,778 (19.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 2,940,194 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 233,718 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ne_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ne_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `ne_nssp_wide.csv` matches the long table | PASS | 64,999 cells; missing 0, unexpected 0, differing 0 |
| `ne_nwss_wide.csv` matches the long table | PASS | 26,592 cells; missing 0, unexpected 0, differing 0 |
| `ne_all_sources_wide.csv` matches the long table | PASS | 94,480 cells; missing 0, unexpected 0, differing 0 |
| `ne_all_sources_wide.csv` census columns match `ne_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
