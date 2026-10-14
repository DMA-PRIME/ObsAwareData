# Missouri (MO): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 29
- Emergency-department regions (CDC health service areas): 27
- Wastewater sampling sites: 81 (with COVID-19 data: 81; influenza A: 74; RSV: 67)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-09 (86 releases); ED visits 2026-06-12 to 2026-10-07 (16 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mo_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `mo_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `mo_long_latest_2022.csv` | 18,526 | 15 | 4.2 |
| `mo_long_latest_2023.csv` | 31,610 | 15 | 7.5 |
| `mo_long_latest_2024.csv` | 36,164 | 15 | 8.5 |
| `mo_long_latest_2025.csv` | 36,581 | 15 | 8.6 |
| `mo_long_latest_2026.csv` | 23,468 | 15 | 5.6 |
| `mo_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `mo_nssp_wide.csv` | 5,880 | 30 | 2.3 |
| `mo_nwss_wide.csv` | 11,996 | 24 | 2.8 |
| `mo_all_sources_wide.csv` | 322 | 2,045 | 4.1 |
| `mo_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 28 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 28 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 28 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 0 | none | none |
| Wastewater (NWSS) | covid | 81 | 2022-01-01 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 74 | 2022-09-03 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 67 | 2023-05-13 | 2026-10-03 |

## Reliability flags

Number of rows in `mo_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 684 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 667 | 25 | 0 | 55 | 10 | 209 |
| NHSN | hospital_reporting_count | 747 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 12,152 | 0 | 5,488 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 7,254 | 10,386 | 0 | 0 | 5,880 | 0 |
| NSSP | ed_visit_percent_smoothed | 7,373 | 1,352 | 0 | 725 | 14,070 | 0 |
| NSSP | participation_status | 1,050 | 0 | 4,620 | 0 | 0 | 0 |
| NWSS | participation_status | 22,997 | 0 | 1,589 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 22,529 | 0 | 0 | 2,057 | 0 | 0 |
| NWSS | wastewater_activity_level | 22,529 | 0 | 0 | 2,057 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MO |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 66 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 50% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.34 |
| Wastewater: same, influenza A | 0.05 |
| Wastewater: same, RSV | 0.36 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`mo_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,168,194 rows covering 147,006 distinct values. Of those, 36,583 (24.9%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 17 | 2026-06-12 | 2026-10-07 | 1,150,390 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 714,900 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `mo_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mo_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `mo_nssp_wide.csv` matches the long table | PASS | 70,350 cells; missing 0, unexpected 0, differing 0 |
| `mo_nwss_wide.csv` matches the long table | PASS | 73,758 cells; missing 0, unexpected 0, differing 0 |
| `mo_all_sources_wide.csv` matches the long table | PASS | 147,006 cells; missing 0, unexpected 0, differing 0 |
| `mo_all_sources_wide.csv` census columns match `mo_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
