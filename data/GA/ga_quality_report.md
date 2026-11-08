# Georgia (GA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 13
- Emergency-department regions (CDC health service areas): 42
- Wastewater sampling sites: 31 (with COVID-19 data: 31; influenza A: 30; RSV: 29)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-11-06 (87 releases); ED visits 2025-08-15 to 2026-11-04 (52 releases); wastewater 2026-08-07 to 2026-11-06 (14 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ga_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ga_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ga_long_latest_2022.csv` | 9,817 | 15 | 2.3 |
| `ga_long_latest_2023.csv` | 33,098 | 15 | 8.0 |
| `ga_long_latest_2024.csv` | 35,801 | 15 | 8.6 |
| `ga_long_latest_2025.csv` | 36,299 | 15 | 8.7 |
| `ga_long_latest_2026.csv` | 31,708 | 15 | 7.6 |
| `ga_nhsn_wide.csv` | 326 | 24 | 0.1 |
| `ga_nssp_wide.csv` | 9,202 | 30 | 3.6 |
| `ga_nwss_wide.csv` | 4,655 | 24 | 1.2 |
| `ga_all_sources_wide.csv` | 326 | 1,613 | 3.9 |
| `ga_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-31 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-09-05 | 2026-10-31 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-31 |
| Emergency department visits (NSSP) | covid | 37 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 37 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 37 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 37 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 31 | 2022-04-16 | 2026-10-31 |
| Wastewater (NWSS) | influenza | 30 | 2022-07-02 | 2026-10-31 |
| Wastewater (NWSS) | rsv | 29 | 2022-07-02 | 2026-10-31 |

## Reliability flags

Number of rows in `ga_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 695 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 700 | 19 | 0 | 46 | 4 | 209 |
| NHSN | hospital_reporting_count | 765 | 4 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 19,167 | 0 | 8,439 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 18,977 | 8,329 | 0 | 0 | 9,502 | 0 |
| NSSP | ed_visit_percent_smoothed | 19,714 | 436 | 0 | 2,410 | 14,248 | 0 |
| NSSP | participation_status | 1,498 | 0 | 7,490 | 0 | 0 | 0 |
| NWSS | participation_status | 10,484 | 0 | 928 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 10,725 | 0 | 0 | 687 | 0 | 0 |
| NWSS | wastewater_activity_level | 10,725 | 0 | 0 | 687 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for GA |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 91 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 72% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 35% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.57 |
| Wastewater: same, influenza A | 0.60 |
| Wastewater: same, RSV | 0.45 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`ga_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 6,190,591 rows covering 147,380 distinct values. Of those, 36,592 (24.8%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 124 | 2025-04-04 | 2026-11-06 | 326,268 |
| NSSP | 57 | 2025-08-15 | 2026-11-04 | 5,414,710 |
| NWSS | 14 | 2026-08-07 | 2026-11-06 | 449,613 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ga_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ga_nhsn_wide.csv` matches the long table | PASS | 2,934 cells; missing 0, unexpected 0, differing 0 |
| `ga_nssp_wide.csv` matches the long table | PASS | 110,210 cells; missing 0, unexpected 0, differing 0 |
| `ga_nwss_wide.csv` matches the long table | PASS | 34,236 cells; missing 0, unexpected 0, differing 0 |
| `ga_all_sources_wide.csv` matches the long table | PASS | 147,380 cells; missing 0, unexpected 0, differing 0 |
| `ga_all_sources_wide.csv` census columns match `ga_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 326 weeks, 2020-08-08 to 2026-10-31 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
