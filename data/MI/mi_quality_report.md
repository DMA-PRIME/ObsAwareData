# Michigan (MI): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 26
- Emergency-department regions (CDC health service areas): 25
- Wastewater sampling sites: 72 (with COVID-19 data: 63; influenza A: 55; RSV: 52)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-21 (84 releases); ED visits 2025-08-15 to 2026-10-21 (50 releases); wastewater 2026-08-07 to 2026-10-23 (12 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `mi_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `mi_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `mi_long_latest_2022.csv` | 11,338 | 15 | 2.6 |
| `mi_long_latest_2023.csv` | 25,871 | 15 | 6.2 |
| `mi_long_latest_2024.csv` | 31,880 | 15 | 7.5 |
| `mi_long_latest_2025.csv` | 26,237 | 15 | 6.3 |
| `mi_long_latest_2026.csv` | 23,751 | 15 | 5.6 |
| `mi_nhsn_wide.csv` | 324 | 24 | 0.1 |
| `mi_nssp_wide.csv` | 5,512 | 30 | 2.1 |
| `mi_nwss_wide.csv` | 10,109 | 24 | 2.1 |
| `mi_all_sources_wide.csv` | 324 | 1,685 | 3.3 |
| `mi_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-08-08 | 2026-10-17 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-17 |
| Emergency department visits (NSSP) | covid | 24 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | influenza | 24 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | rsv | 24 | 2022-10-01 | 2026-10-17 |
| Emergency department visits (NSSP) | combined | 24 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 63 | 2022-01-01 | 2026-10-17 |
| Wastewater (NWSS) | influenza | 55 | 2022-04-23 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 52 | 2022-04-23 | 2026-10-17 |

## Reliability flags

Number of rows in `mi_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 682 | 0 | 81 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 678 | 36 | 0 | 49 | 0 | 209 |
| NHSN | hospital_reporting_count | 763 | 0 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 15,052 | 0 | 1,484 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 13,984 | 3,800 | 0 | 0 | 4,264 | 0 |
| NSSP | ed_visit_percent_smoothed | 14,641 | 896 | 0 | 1,823 | 4,688 | 0 |
| NSSP | participation_status | 3,392 | 0 | 1,908 | 0 | 0 | 0 |
| NWSS | participation_status | 14,766 | 0 | 2,196 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 14,634 | 0 | 0 | 2,328 | 0 | 0 |
| NWSS | wastewater_activity_level | 14,634 | 0 | 0 | 2,328 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for MI |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 121 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.57 |
| Wastewater: same, influenza A | 0.19 |
| Wastewater: same, RSV | 0.33 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`mi_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 4,039,154 rows covering 119,734 distinct values. Of those, 42,603 (35.6%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 120 | 2025-04-04 | 2026-10-23 | 314,550 |
| NSSP | 55 | 2025-08-15 | 2026-10-21 | 3,137,057 |
| NWSS | 12 | 2026-08-07 | 2026-10-23 | 587,547 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `mi_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `mi_nhsn_wide.csv` matches the long table | PASS | 2,916 cells; missing 0, unexpected 0, differing 0 |
| `mi_nssp_wide.csv` matches the long table | PASS | 65,932 cells; missing 0, unexpected 0, differing 0 |
| `mi_nwss_wide.csv` matches the long table | PASS | 50,886 cells; missing 0, unexpected 0, differing 0 |
| `mi_all_sources_wide.csv` matches the long table | PASS | 119,734 cells; missing 0, unexpected 0, differing 0 |
| `mi_all_sources_wide.csv` census columns match `mi_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 324 weeks, 2020-08-08 to 2026-10-17 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
