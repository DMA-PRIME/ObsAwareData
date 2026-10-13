# South Dakota (SD): data quality report

Generated from the published files in this folder. Overall result: **all checks passed**.

## Summary

- State FIPS code: 46
- Emergency-department regions (CDC health service areas): 15
- Wastewater sampling sites: 6 (with COVID-19 data: 6; influenza A: 5; RSV: 5)
- Source snapshot dates used for the latest values: hospital admissions 2026-10-02; ED visits 2026-09-30; wastewater 2026-10-02

## Files

| File | Rows | Columns | Size (MB) |
|---|---|---|---|
| `sd_long_latest_2020.csv` | 189 | 16 | 0.0 |
| `sd_long_latest_2021.csv` | 468 | 16 | 0.1 |
| `sd_long_latest_2022.csv` | 3,496 | 16 | 0.9 |
| `sd_long_latest_2023.csv` | 11,054 | 16 | 2.9 |
| `sd_long_latest_2024.csv` | 11,327 | 16 | 3.0 |
| `sd_long_latest_2025.csv` | 11,840 | 16 | 3.1 |
| `sd_long_latest_2026.csv` | 9,492 | 16 | 2.4 |
| `sd_nhsn_wide.csv` | 321 | 24 | 0.1 |
| `sd_nssp_wide.csv` | 3,344 | 30 | 1.4 |
| `sd_nwss_wide.csv` | 714 | 24 | 0.2 |
| `sd_all_sources_wide.csv` | 321 | 521 | 1.4 |
| `sd_census_context.csv` | 24 | 6 | 0.0 |

## Coverage

A week counts as "with data" when the primary measure (weekly admissions, ED visit percent, or wastewater activity level) has a value, including values flagged low-coverage or anomalous.

| Source | Pathogen | Regions or sites with data | First week with data | Last week with data |
|---|---|---|---|---|
| Hospital admissions (NHSN) | covid | 1 | 2020-08-08 | 2026-09-26 |
| Hospital admissions (NHSN) | influenza | 1 | 2020-10-03 | 2026-09-26 |
| Hospital admissions (NHSN) | rsv | 1 | 2024-08-10 | 2026-09-26 |
| Emergency department visits (NSSP) | covid | 1 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | influenza | 1 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | rsv | 1 | 2022-10-01 | 2026-09-26 |
| Emergency department visits (NSSP) | combined | 0 | none | none |
| Wastewater (NWSS) | covid | 6 | 2022-06-04 | 2026-09-26 |
| Wastewater (NWSS) | influenza | 5 | 2023-04-29 | 2026-09-26 |
| Wastewater (NWSS) | rsv | 5 | 2023-04-29 | 2026-09-26 |

## Reliability flags

Number of rows in `sd_long_latest_<year>.csv` (all years) by source, measure, and `observation_state` (see `DATA_DICTIONARY.md`).

| Source | Measure | observed_valid | observed_zero | observed_low_coverage | flagged_anomalous | incidental_missing | structural_absent |
|---|---|---|---|---|---|---|---|
| NHSN | coverage_status | 680 | 0 | 74 | 0 | 0 | 209 |
| NHSN | hospital_admission_count | 593 | 118 | 0 | 35 | 8 | 209 |
| NHSN | hospital_reporting_count | 746 | 8 | 0 | 0 | 0 | 209 |
| NSSP | ed_trend_category | 627 | 0 | 9,405 | 0 | 0 | 0 |
| NSSP | ed_visit_percent | 568 | 59 | 0 | 0 | 12,749 | 0 |
| NSSP | ed_visit_percent_smoothed | 535 | 25 | 0 | 67 | 12,749 | 0 |
| NSSP | participation_status | 1,045 | 0 | 2,090 | 0 | 0 | 0 |
| NWSS | participation_status | 1,490 | 0 | 196 | 0 | 0 | 0 |
| NWSS | wastewater_activity_category | 1,639 | 0 | 0 | 47 | 0 | 0 |
| NWSS | wastewater_activity_level | 1,639 | 0 | 0 | 47 | 0 | 0 |

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

Every published version of every value, one row per (source, week, region, pathogen, measure, source snapshot): 2,145,248 rows covering 47,866 distinct values. Of those, 2,886 (6.0%) took more than one distinct value across snapshots, i.e. were revised after first publication.

| Source | Snapshots | Earliest snapshot | Latest snapshot | Rows |
|---|---|---|---|---|
| NHSN | 114 | 2025-04-04 | 2026-10-02 | 297,108 |
| NSSP | 52 | 2025-08-15 | 2026-09-30 | 1,805,714 |
| NWSS | 9 | 2026-08-07 | 2026-10-02 | 42,426 |

## Consistency checks

| Check | Result | Detail |
|---|---|---|
| `sd_long_latest_<year>.csv`: each file holds only weeks ending in its year | PASS | 7 files (2020, 2021, 2022, 2023, 2024, 2025, 2026); 0 rows in the wrong file |
| Long table: one row per (source, week, region type, region, pathogen, measure) | PASS | 0 duplicate keys |
| `sd_nhsn_wide.csv` matches the long table | PASS | 2,889 cells; missing 0, unexpected 0, differing 0 |
| `sd_nssp_wide.csv` matches the long table | PASS | 39,919 cells; missing 0, unexpected 0, differing 0 |
| `sd_nwss_wide.csv` matches the long table | PASS | 5,058 cells; missing 0, unexpected 0, differing 0 |
| `sd_all_sources_wide.csv` matches the long table | PASS | 47,866 cells; missing 0, unexpected 0, differing 0 |
| `sd_all_sources_wide.csv` census columns match `sd_census_context.csv` | PASS | 24 columns, constant across all weeks |
| All-sources table has one row per week, weekly with no gaps, covering every week in the long table | PASS | 321 weeks, 2020-08-08 to 2026-09-26 |
| Revision history: one row per (key, source snapshot) | PASS | 0 duplicates |
| Every latest-table row appears, with the same value, in the revision history | PASS | 0 missing, 0 differing |
