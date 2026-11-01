# Georgia (GA): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 13
- Emergency-department regions (CDC health service areas): 42
- Wastewater sampling sites: 31 (with COVID-19 data: 31; influenza A: 30; RSV: 29)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-30 (85 releases); ED visits 2025-08-15 to 2026-10-28 (51 releases); wastewater 2026-08-07 to 2026-10-30 (13 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `ga_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `ga_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `ga_long_latest_2022.csv` | 9,817 | 15 | 2.3 |
| `ga_long_latest_2023.csv` | 33,098 | 15 | 8.0 |
| `ga_long_latest_2024.csv` | 35,801 | 15 | 8.6 |
| `ga_long_latest_2025.csv` | 36,299 | 15 | 8.7 |
| `ga_long_latest_2026.csv` | 30,941 | 15 | 7.4 |
| `ga_nhsn_wide.csv` | 325 | 24 | 0.1 |
| `ga_nssp_wide.csv` | 9,159 | 30 | 3.6 |
| `ga_nwss_wide.csv` | 4,627 | 24 | 1.2 |
| `ga_all_sources_wide.csv` | 325 | 1,613 | 3.9 |
| `ga_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-24 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-09-05 | 2026-10-24 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-24 |
| Emergency department visits (NSSP) | covid | 37 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | influenza | 37 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | rsv | 37 | 2022-10-01 | 2026-10-10 |
| Emergency department visits (NSSP) | combined | 37 | 2022-10-01 | 2024-09-28 |
| Wastewater (NWSS) | covid | 31 | 2022-04-16 | 2026-10-24 |
| Wastewater (NWSS) | influenza | 30 | 2022-07-02 | 2026-10-24 |
| Wastewater (NWSS) | rsv | 29 | 2022-07-02 | 2026-10-24 |

## Reliability flags

Number of rows in `ga_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 692 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 698 | 19 | 0 | 45 | 4 | 209 |
| NHSN | hospital_reporting_count | 762 | 4 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 19,167 | 0 | 8,310 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 18,968 | 8,338 | 0 | 0 | 9,330 | 0 |
| NSSP | ed_visit_percent_smoothed | 19,738 | 429 | 0 | 2,393 | 14,076 | 0 |
| NSSP | participation_status | 1,491 | 0 | 7,455 | 0 | 0 | 0 |
| NWSS | participation_status | 10,403 | 0 | 928 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 10,654 | 0 | 0 | 677 | 0 | 0 |
| NWSS | wastewater_activity_level | 10,654 | 0 | 0 | 677 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 6,040,895 rows covering 146,613 distinct values. Of those, 35,942 (24.5%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 122 | 2025-04-04 | 2026-10-30 | 320,400 |
| NSSP | 56 | 2025-08-15 | 2026-10-28 | 5,304,500 |
| NWSS | 13 | 2026-08-07 | 2026-10-30 | 415,995 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `ga_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `ga_nhsn_wide.csv` matches the long table | PASS | 2,925 cells; missing 0, unexpected 0, differing 0 |
| `ga_nssp_wide.csv` matches the long table | PASS | 109,695 cells; missing 0, unexpected 0, differing 0 |
| `ga_nwss_wide.csv` matches the long table | PASS | 33,993 cells; missing 0, unexpected 0, differing 0 |
| `ga_all_sources_wide.csv` matches the long table | PASS | 146,613 cells; missing 0, unexpected 0, differing 0 |
| `ga_all_sources_wide.csv` census columns match `ga_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 325 weeks, 2020-08-08 to 2026-10-24 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
