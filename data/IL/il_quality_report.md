# Illinois (IL): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 17
- Emergency-department regions (CDC health service areas): 35
- Wastewater sampling sites: 89 (with COVID-19 data: 89; influenza A: 87; RSV: 85)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-20 (98 releases); ED visits 2025-08-15 to 2026-11-18 (54 releases); wastewater 2026-08-07 to 2026-11-20 (16 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `il_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `il_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `il_long_latest_2022.csv` | 19,096 | 15 | 4.3 |
| `il_long_latest_2023.csv` | 55,394 | 15 | 12.7 |
| `il_long_latest_2024.csv` | 57,248 | 15 | 13.1 |
| `il_long_latest_2025.csv` | 55,901 | 15 | 12.8 |
| `il_long_latest_2026.csv` | 48,905 | 15 | 11.2 |
| `il_nhsn_wide.csv` | 328 | 24 | 0.1 |
| `il_nssp_wide.csv` | 7,776 | 30 | 3.0 |
| `il_nwss_wide.csv` | 17,755 | 24 | 4.9 |
| `il_all_sources_wide.csv` | 328 | 2,471 | 6.4 |
| `il_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-11-14 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-17 | 2026-11-14 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-11-14 |
| Emergency department visits (NSSP) | covid | 34 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | influenza | 34 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | rsv | 34 | 2022-10-01 | 2026-11-07 |
| Emergency department visits (NSSP) | combined | 34 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 89 | 2022-01-01 | 2026-11-14 |
| Wastewater (NWSS) | influenza | 87 | 2022-08-06 | 2026-11-14 |
| Wastewater (NWSS) | rsv | 85 | 2022-08-06 | 2026-11-14 |

## Reliability flags

Number of rows in `il_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 704 | 0 | 71 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 704 | 14 | 0 | 47 | 10 | 209 |
| NHSN | hospital_reporting_count | 765 | 10 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 20,628 | 0 | 2,700 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 18,647 | 6,853 | 0 | 0 | 5,604 | 0 |
| NSSP | ed_visit_percent_smoothed | 20,695 | 615 | 0 | 2,470 | 7,324 | 0 |
| NSSP | participation_status | 3,888 | 0 | 3,672 | 0 | 0 | 0 |
| NWSS | participation_status | 39,826 | 0 | 7,225 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 43,578 | 0 | 0 | 3,473 | 0 | 0 |
| NWSS | wastewater_activity_level | 43,578 | 0 | 0 | 3,473 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for IL |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 109 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 103% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 40% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.90 |
| Wastewater: same, influenza A | 0.89 |
| Wastewater: same, RSV | 0.88 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`il_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 7,238,123 rows covering 237,201 distinct values. Of those, 70,680 (29.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 128 | 2025-04-04 | 2026-11-20 | 338,058 |
| NSSP | 59 | 2025-08-15 | 2026-11-18 | 4,717,295 |
| NWSS | 16 | 2026-08-07 | 2026-11-20 | 2,182,770 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `il_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `il_nhsn_wide.csv` matches the long table | PASS | 2,952 cells; missing 0, unexpected 0, differing 0 |
| `il_nssp_wide.csv` matches the long table | PASS | 93,096 cells; missing 0, unexpected 0, differing 0 |
| `il_nwss_wide.csv` matches the long table | PASS | 141,153 cells; missing 0, unexpected 0, differing 0 |
| `il_all_sources_wide.csv` matches the long table | PASS | 237,201 cells; missing 0, unexpected 0, differing 0 |
| `il_all_sources_wide.csv` census columns match `il_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 328 weeks, 2020-08-08 to 2026-11-14 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
