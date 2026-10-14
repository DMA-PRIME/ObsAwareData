# Idaho (ID): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 16
- Emergency-department regions (CDC health service areas): 12
- Wastewater sampling sites: 21 (with COVID-19 data: 21; influenza A: 14; RSV: 5)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-09 (88 releases); ED visits 2025-08-15 to 2026-10-07 (48 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `id_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `id_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `id_long_latest_2022.csv` | 4,510 | 15 | 1.0 |
| `id_long_latest_2023.csv` | 11,996 | 15 | 2.8 |
| `id_long_latest_2024.csv` | 10,385 | 15 | 2.5 |
| `id_long_latest_2025.csv` | 10,400 | 15 | 2.5 |
| `id_long_latest_2026.csv` | 8,180 | 15 | 1.9 |
| `id_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `id_nssp_wide.csv` | 2,730 | 30 | 1.0 |
| `id_nwss_wide.csv` | 1,902 | 24 | 0.4 |
| `id_all_sources_wide.csv` | 322 | 593 | 1.3 |
| `id_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-10 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 13 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 13 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 13 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 13 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 21 | 2022-01-01 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 14 | 2022-03-05 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 5 | 2022-03-05 | 2026-10-03 |

## Reliability flags

Number of rows in `id_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 680 | 0 | 77 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 579 | 121 | 0 | 48 | 9 | 209 |
| NHSN | hospital_reporting_count | 748 | 9 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 6,930 | 0 | 1,260 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 6,471 | 3,084 | 0 | 0 | 1,365 | 0 |
| NSSP | ed_visit_percent_smoothed | 6,929 | 151 | 0 | 1,005 | 2,835 | 0 |
| NSSP | participation_status | 1,260 | 0 | 1,260 | 0 | 0 | 0 |
| NWSS | participation_status | 2,998 | 0 | 562 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 2,823 | 0 | 0 | 737 | 0 | 0 |
| NWSS | wastewater_activity_level | 2,823 | 0 | 0 | 737 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for ID |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 29 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.26 |
| Wastewater: same, influenza A | 0.02 |
| Wastewater: same, RSV | 1.00 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`id_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,905,872 rows covering 46,128 distinct values. Of those, 13,859 (30.0%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,497,920 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 105,048 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `id_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `id_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `id_nssp_wide.csv` matches the long table | PASS | 32,550 cells; missing 0, unexpected 0, differing 0 |
| `id_nwss_wide.csv` matches the long table | PASS | 10,680 cells; missing 0, unexpected 0, differing 0 |
| `id_all_sources_wide.csv` matches the long table | PASS | 46,128 cells; missing 0, unexpected 0, differing 0 |
| `id_all_sources_wide.csv` census columns match `id_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
