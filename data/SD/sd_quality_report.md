# South Dakota (SD): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 46
- Emergency-department regions (CDC health service areas): 15
- Wastewater sampling sites: 6 (with COVID-19 data: 6; influenza A: 5; RSV: 5)
- Source releases cited by the latest values (each row cites the release that first published its current value): hospital admissions 2025-04-04 to 2026-10-09 (85 releases); ED visits 2025-08-15 to 2026-10-07 (48 releases); wastewater 2026-08-07 to 2026-10-09 (10 releases)

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `sd_long_latest_2020.csv` | 189 | 15 | 0.0 |
| `sd_long_latest_2021.csv` | 468 | 15 | 0.1 |
| `sd_long_latest_2022.csv` | 3,496 | 15 | 0.8 |
| `sd_long_latest_2023.csv` | 11,054 | 15 | 2.8 |
| `sd_long_latest_2024.csv` | 11,327 | 15 | 2.8 |
| `sd_long_latest_2025.csv` | 11,840 | 15 | 2.9 |
| `sd_long_latest_2026.csv` | 9,719 | 15 | 2.4 |
| `sd_nhsn_wide.csv` | 322 | 24 | 0.1 |
| `sd_nssp_wide.csv` | 3,360 | 30 | 1.4 |
| `sd_nwss_wide.csv` | 717 | 24 | 0.2 |
| `sd_all_sources_wide.csv` | 322 | 521 | 1.4 |
| `sd_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-10-03 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-03 | 2026-10-03 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-10-03 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-10-03 |
| Emergency department visits (NSSP) | combined | 0 | none | none |
| Wastewater (NWSS) | covid | 6 | 2022-06-04 | 2026-10-03 |
| Wastewater (NWSS) | influenza | 5 | 2023-04-29 | 2026-10-03 |
| Wastewater (NWSS) | rsv | 5 | 2023-04-29 | 2026-10-03 |

## Reliability flags

Number of rows in `sd_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 683 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 594 | 118 | 0 | 37 | 8 | 209 |
| NHSN | hospital_reporting_count | 749 | 8 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 630 | 0 | 9,450 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 572 | 58 | 0 | 0 | 12,810 | 0 |
| NSSP | ed_visit_percent_smoothed | 537 | 25 | 0 | 68 | 12,810 | 0 |
| NSSP | participation_status | 1,050 | 0 | 2,100 | 0 | 0 | 0 |
| NWSS | participation_status | 1,499 | 0 | 196 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,646 | 0 | 0 | 49 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,646 | 0 | 0 | 49 | 0 | 0 |

Thresholds behind `observed_low_coverage` and `flagged_anomalous` for this state (method in `METHODS.md`):

| Rule | Value used for SD |
|---|---|
| Hospital admissions: `coverage_status = reduced_participation` when fewer reporting hospitals than | 28 |
| Hospital admissions: `flagged_anomalous` when week-over-week change is at least | 134% |
| ED visits: smoothed percent `flagged_anomalous` when week-over-week change is at least | 50% |
| Wastewater: `reduced_participation` when a site's reporting coverage ratio is below (COVID-19) | 0.61 |
| Wastewater: same, influenza A | 0.86 |
| Wastewater: same, RSV | 0.86 |

Census margin-of-error variables carrying the Census Bureau's negative placeholder code instead of a real value: `total_population_moe`.

## Revision history (`sd_long_all_versions*.csv.gz`)

Location: GitHub Release assets, not stored in the repository. `metadata/release_assets.csv` lists this state's files in order, with download links and checksums: one `full` file, then one `increment` per later release holding only the source snapshots first published in it. Concatenating them in that order, keeping only the first header line, gives the complete table described here.

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,196,239 rows covering 48,093 distinct values. Of those, 2,993 (6.2%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 116 | 2025-04-04 | 2026-10-09 | 302,904 |
| NSSP | 53 | 2025-08-15 | 2026-10-07 | 1,845,824 |
| NWSS | 10 | 2026-08-07 | 2026-10-09 | 47,511 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `sd_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `sd_nhsn_wide.csv` matches the long table | PASS | 2,898 cells; missing 0, unexpected 0, differing 0 |
| `sd_nssp_wide.csv` matches the long table | PASS | 40,110 cells; missing 0, unexpected 0, differing 0 |
| `sd_nwss_wide.csv` matches the long table | PASS | 5,085 cells; missing 0, unexpected 0, differing 0 |
| `sd_all_sources_wide.csv` matches the long table | PASS | 48,093 cells; missing 0, unexpected 0, differing 0 |
| `sd_all_sources_wide.csv` census columns match `sd_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 322 weeks, 2020-08-08 to 2026-10-03 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
