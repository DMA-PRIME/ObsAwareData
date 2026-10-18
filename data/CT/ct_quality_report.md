# Connecticut (CT): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 09
- Emergency-department regions (CDC health service areas): 4
- Wastewater sampling sites: 17 (with COVID-19 data: 17; influenza A: 14; RSV: 14)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-14 (82 releases); ED visits 2025-08-15 to 2026-10-14 (49 releases); wastewater 2026-08-07 to 2026-10-16 (11 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ct_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ct_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ct_long_latest_2022.csv` | 2,251 | 15 | 0.5 |
| `ct_long_latest_2023.csv` | 5,093 | 15 | 1.1 |
| `ct_long_latest_2024.csv` | 6,491 | 15 | 1.5 |
| `ct_long_latest_2025.csv` | 8,168 | 15 | 1.8 |
| `ct_long_latest_2026.csv` | 7,603 | 15 | 1.7 |
| `ct_nhsn_wide.csv` | 323 | 24 | 0.1 |
| `ct_nssp_wide.csv` | 1,055 | 30 | 0.4 |
| `ct_nwss_wide.csv` | 2,550 | 24 | 0.6 |
| `ct_all_sources_wide.csv` | 323 | 431 | 0.9 |
| `ct_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-10 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-09-26 | 2026-10-10 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-10 |
| Emergency department visits (NSSP) | covid | 5 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 5 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 5 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 5 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 17 | 2022-05-07 | 2026-10-10 |
| Wastewater (NWSS) | influenza | 14 | 2023-11-04 | 2026-10-10 |
| Wastewater (NWSS) | rsv | 14 | 2023-10-28 | 2026-10-10 |

## Reliability flags

Number of rows in `ct_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 722 | 0 | 38 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 629 | 77 | 0 | 46 | 8 | 209 |
| NHSN | hospital_reporting_count | 752 | 8 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 3,165 | 0 | 0 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 3,437 | 253 | 0 | 0 | 530 | 0 |
| NSSP | ed_visit_percent_smoothed | 3,091 | 120 | 0 | 479 | 530 | 0 |
| NSSP | participation_status | 844 | 0 | 0 | 0 | 0 | 0 |
| NWSS | participation_status | 3,204 | 0 | 1,765 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 4,495 | 0 | 0 | 474 | 0 | 0 |
| NWSS | wastewater_activity_level | 4,495 | 0 | 0 | 474 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for CT |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 29 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 92% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.84 |
| Wastewater: same, influenza A | 0.98 |
| Wastewater: same, RSV | 0.98 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ct_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 1,050,115 rows covering 30,263 distinct values. Of those, 9,313 (30.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 118 | 2025-04-04 | 2026-10-16 | 308,718 |
| NSSP | 54 | 2025-08-15 | 2026-10-14 | 582,625 |
| NWSS | 11 | 2026-08-07 | 2026-10-16 | 158,772 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ct_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ct_nhsn_wide.csv` matches the long table | PASS | 2,907 cells; missing 0, unexpected 0, differing 0 |
| `ct_nssp_wide.csv` matches the long table | PASS | 12,449 cells; missing 0, unexpected 0, differing 0 |
| `ct_nwss_wide.csv` matches the long table | PASS | 14,907 cells; missing 0, unexpected 0, differing 0 |
| `ct_all_sources_wide.csv` matches the long table | PASS | 30,263 cells; missing 0, unexpected 0, differing 0 |
| `ct_all_sources_wide.csv` census columns match `ct_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 323 weeks, 2020-08-08 to 2026-10-10 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
