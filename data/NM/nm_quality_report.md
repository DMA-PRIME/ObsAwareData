# New Mexico (NM): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 35
- Emergency-department regions (CDC health service areas): 13
- Wastewater sampling sites: 14 (with COVID-19 data: 14; influenza A: 2; RSV: 2)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-07 (79 releases); ED visits 2025-08-15 to 2026-10-07 (48 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `nm_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `nm_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `nm_long_latest_2022.csv` | 3,499 | 15 | 0.8 |
| `nm_long_latest_2023.csv` | 10,523 | 15 | 2.4 |
| `nm_long_latest_2024.csv` | 10,748 | 15 | 2.5 |
| `nm_long_latest_2025.csv` | 10,802 | 15 | 2.5 |
| `nm_long_latest_2026.csv` | 8,291 | 15 | 1.9 |
| `nm_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `nm_nssp_wide.csv` | 2,940 | 30 | 1.1 |
| `nm_nwss_wide.csv` | 1,660 | 24 | 0.3 |
| `nm_all_sources_wide.csv` | 322 | 485 | 1.2 |
| `nm_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-24 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-10-12 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 12 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 12 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 12 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 12 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 14 | 2022-05-07 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 2 | 2023-12-02 | 2026-09-12 |
| Wastewater (NWSS) | rsv | 2 | 2023-12-02 | 2026-09-12 |

## Reliability flags

Number of rows in `nm_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 680 | 0 | 77 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 605 | 69 | 0 | 63 | 20 | 209 |
| NHSN | hospital_reporting_count | 737 | 20 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,930 | 0 | 1,890 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 6,595 | 2,225 | 0 | 0 | 2,940 | 0 |
| NSSP | ed_visit_percent_smoothed | 6,904 | 261 | 0 | 815 | 3,780 | 0 |
| NSSP | participation_status | 1,890 | 0 | 840 | 0 | 0 | 0 |
| NWSS | participation_status | 1,858 | 0 | 326 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 2,048 | 0 | 0 | 136 | 0 | 0 |
| NWSS | wastewater_activity_level | 2,048 | 0 | 0 | 136 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for NM |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 18 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.24 |
| Wastewater: same, influenza A | 0.92 |
| Wastewater: same, RSV | 0.91 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`nm_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,981,136 rows covering 44,520 distinct values. Of those, 12,031 (27.0%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,613,888 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 64,344 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `nm_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `nm_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `nm_nssp_wide.csv` matches the long table | PASS | 35,070 cells; missing 0, unexpected 0, differing 0 |
| `nm_nwss_wide.csv` matches the long table | PASS | 6,552 cells; missing 0, unexpected 0, differing 0 |
| `nm_all_sources_wide.csv` matches the long table | PASS | 44,520 cells; missing 0, unexpected 0, differing 0 |
| `nm_all_sources_wide.csv` census columns match `nm_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
