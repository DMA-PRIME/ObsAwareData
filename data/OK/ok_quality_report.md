# Oklahoma (OK): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 40
- Emergency-department regions (CDC health service areas): 26
- Wastewater sampling sites: 21 (with COVID-19 data: 21; influenza A: 18; RSV: 18)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-30 (97 releases); ED visits 2025-08-15 to 2026-10-28 (51 releases); wastewater 2026-08-07 to 2026-10-30 (13 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ok_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ok_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ok_long_latest_2022.csv` | 8,293 | 15 | 1.9 |
| `ok_long_latest_2023.csv` | 24,245 | 15 | 5.7 |
| `ok_long_latest_2024.csv` | 24,935 | 15 | 5.9 |
| `ok_long_latest_2025.csv` | 21,182 | 15 | 5.1 |
| `ok_long_latest_2026.csv` | 17,834 | 15 | 4.3 |
| `ok_nhsn_wide.csv` | 325 | 24 | 0.1 |
| `ok_nssp_wide.csv` | 5,751 | 30 | 2.4 |
| `ok_nwss_wide.csv` | 3,249 | 24 | 0.9 |
| `ok_all_sources_wide.csv` | 325 | 1,031 | 2.7 |
| `ok_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-24 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-10 | 2026-10-24 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-24 |
| Emergency department visits (NSSP) | covid | 9 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | influenza | 9 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | rsv | 9 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | combined | 9 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 21 | 2022-01-01 | 2026-10-24 |
| Wastewater (NWSS) | influenza | 18 | 2022-01-01 | 2026-10-17 |
| Wastewater (NWSS) | rsv | 18 | 2022-08-20 | 2026-10-24 |

## Reliability flags

Number of rows in `ok_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 693 | 0 | 73 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 669 | 36 | 0 | 52 | 9 | 209 |
| NHSN | hospital_reporting_count | 757 | 9 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 5,538 | 0 | 11,715 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 4,804 | 1,892 | 0 | 0 | 16,308 | 0 |
| NSSP | ed_visit_percent_smoothed | 5,435 | 163 | 0 | 672 | 16,734 | 0 |
| NSSP | participation_status | 213 | 0 | 5,325 | 0 | 0 | 0 |
| NWSS | participation_status | 7,156 | 0 | 1,318 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 7,536 | 0 | 0 | 938 | 0 | 0 |
| NWSS | wastewater_activity_level | 7,536 | 0 | 0 | 938 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for OK |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 84 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 100% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 39% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.59 |
| Wastewater: same, influenza A | 0.57 |
| Wastewater: same, RSV | 0.50 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ok_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 3,933,635 rows covering 97,146 distinct values. Of those, 12,130 (12.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 122 | 2025-04-04 | 2026-10-30 | 320,400 |
| NSSP | 56 | 2025-08-15 | 2026-10-28 | 3,326,900 |
| NWSS | 13 | 2026-08-07 | 2026-10-30 | 286,335 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ok_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ok_nhsn_wide.csv` matches the long table | PASS | 2,925 cells; missing 0, unexpected 0, differing 0 |
| `ok_nssp_wide.csv` matches the long table | PASS | 68,799 cells; missing 0, unexpected 0, differing 0 |
| `ok_nwss_wide.csv` matches the long table | PASS | 25,422 cells; missing 0, unexpected 0, differing 0 |
| `ok_all_sources_wide.csv` matches the long table | PASS | 97,146 cells; missing 0, unexpected 0, differing 0 |
| `ok_all_sources_wide.csv` census columns match `ok_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 325 weeks, 2020-08-08 to 2026-10-24 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
