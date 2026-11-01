# Texas (TX): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 48
- Emergency-department regions (CDC health service areas): 61
- Wastewater sampling sites: 123 (with COVID-19 data: 123; influenza A: 80; RSV: 80)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-30 (91 releases); ED visits 2025-08-15 to 2026-10-28 (51 releases); wastewater 2026-08-07 to 2026-10-30 (13 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `tx_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `tx_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `tx_long_latest_2022.csv` | 19,351 | 15 | 4.6 |
| `tx_long_latest_2023.csv` | 54,311 | 15 | 13.3 |
| `tx_long_latest_2024.csv` | 58,148 | 15 | 14.1 |
| `tx_long_latest_2025.csv` | 60,737 | 15 | 14.7 |
| `tx_long_latest_2026.csv` | 51,878 | 15 | 12.5 |
| `tx_nhsn_wide.csv` | 325 | 24 | 0.1 |
| `tx_nssp_wide.csv` | 13,206 | 30 | 5.3 |
| `tx_nwss_wide.csv` | 13,674 | 24 | 3.1 |
| `tx_all_sources_wide.csv` | 325 | 3,227 | 6.7 |
| `tx_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-24 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-10-24 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-24 |
| Emergency department visits (NSSP) | covid | 57 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | influenza | 57 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | rsv | 57 | 2022-10-01 | 2026-10-24 |
| Emergency department visits (NSSP) | combined | 57 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 123 | 2022-01-01 | 2026-10-24 |
| Wastewater (NWSS) | influenza | 80 | 2022-03-05 | 2026-10-24 |
| Wastewater (NWSS) | rsv | 80 | 2022-03-05 | 2026-10-24 |

## Reliability flags

Number of rows in `tx_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 691 | 0 | 75 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 696 | 14 | 0 | 46 | 10 | 209 |
| NHSN | hospital_reporting_count | 756 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 34,075 | 0 | 5,543 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 34,204 | 8,204 | 0 | 0 | 10,416 | 0 |
| NSSP | ed_visit_percent_smoothed | 35,221 | 525 | 0 | 4,745 | 12,333 | 0 |
| NSSP | participation_status | 4,260 | 0 | 8,733 | 0 | 0 | 0 |
| NWSS | participation_status | 25,466 | 0 | 2,500 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 25,727 | 0 | 0 | 2,239 | 0 | 0 |
| NWSS | wastewater_activity_level | 25,717 | 10 | 0 | 2,239 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for TX |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 119 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 63% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 33% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.57 |
| Wastewater: same, influenza A | 0.25 |
| Wastewater: same, RSV | 0.25 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`tx_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 9,031,682 rows covering 245,082 distinct values. Of those, 82,199 (33.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 122 | 2025-04-04 | 2026-10-30 | 320,400 |
| NSSP | 56 | 2025-08-15 | 2026-10-28 | 7,652,900 |
| NWSS | 13 | 2026-08-07 | 2026-10-30 | 1,058,382 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `tx_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `tx_nhsn_wide.csv` matches the long table | PASS | 2,925 cells; missing 0, unexpected 0, differing 0 |
| `tx_nssp_wide.csv` matches the long table | PASS | 158,259 cells; missing 0, unexpected 0, differing 0 |
| `tx_nwss_wide.csv` matches the long table | PASS | 83,898 cells; missing 0, unexpected 0, differing 0 |
| `tx_all_sources_wide.csv` matches the long table | PASS | 245,082 cells; missing 0, unexpected 0, differing 0 |
| `tx_all_sources_wide.csv` census columns match `tx_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 325 weeks, 2020-08-08 to 2026-10-24 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
