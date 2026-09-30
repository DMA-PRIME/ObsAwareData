# ObsAwareData: observation-aware weekly respiratory surveillance data for the 50 US states and DC

Weekly COVID-19, influenza, and RSV surveillance data for all 50 states and the District of Columbia, harmonized from three CDC surveillance systems plus US Census context. It is built for forecasting and nowcasting research, so every value carries a **reliability flag** (`observation_state`) and a pointer back to the exact public source release it came from.

| Source | What it measures | Geography | Weeks covered |
|---|---|---|---|
| NHSN Hospital Respiratory Data | New hospital admissions and number of reporting hospitals | State | 2020-08-08 to 2026-08-08 |
| NSSP Emergency Department Visit Trajectories | Percent of ED visits for each pathogen, CDC trend label | State and CDC health service areas (multi-county regions) | 2022-10-01 to 2026-08-08 |
| NWSS Wastewater Viral Activity Level | Wastewater viral activity index and category | Individual wastewater sampling sites | 2022-01-01 to 2026-08-22 |
| Census ACS 5-year 2022 and Population Estimates 2022 | Population and socioeconomic context | State | Static |

Weeks end on Saturday (MMWR week ending date). The latest values reflect the CDC releases available on 2026-08-14 (NHSN, NSSP) and 2026-08-28 (NWSS). Details and links for each source are in [DATA_SOURCES.md](DATA_SOURCES.md).

## What makes this dataset different

- **Reliability flags on every value.** Each value is labeled `observed_valid`, `observed_zero`, `observed_low_coverage`, `flagged_anomalous`, `incidental_missing`, or `structural_absent`, so a missing or questionable week is never silently treated as a real zero or a normal reading.
- **Traceable to the source release.** Each row in the long tables records the CDC release it came from (`source_snapshot_id`, `as_of_date`) and the SHA-256 hash of that raw file.
- **Full revision history for every state.** Every published version of every value across 100 NHSN, 45 NSSP, and 4 NWSS releases is available for all 50 states and DC. These releases are dated April 2025 to August 2026 (NHSN), August 2025 to August 2026 (NSSP), and August 2026 (NWSS), so you can reconstruct what was known on any date in those windows. In South Carolina, for example, about a quarter of all values were revised after first publication. The revision-history files are large, so they are distributed as [GitHub Release assets](https://github.com/DMA-PRIME/ObsAwareData/releases/tag/v1.1.0%2B2026-08-28) rather than in the repository (South Carolina's is also in the repository as an example).
- **No invented aggregation.** Sub-state regions and wastewater sites keep their own columns; nothing is averaged, weighted, or reallocated across geographies.

## Repository layout

```text
ObsAwareData/
├── README.md                 this file
├── DATA_SOURCES.md           where each input comes from
├── DATA_DICTIONARY.md        every file, column, naming rule, and code value
├── METHODS.md                how the tables were built, flag rules, known limitations
├── CHANGELOG.md
├── CITATION.cff
├── LICENSE                   CC BY 4.0
├── metadata/
│   ├── coverage_summary.csv            one row per state: regions, sites, date ranges
│   ├── observation_state_thresholds.csv  per-state thresholds behind the reliability flags
│   ├── manifest.csv                    SHA-256 checksum of every file under data/
│   └── release_assets.csv              download link and SHA-256 of every revision-history file
└── data/
    └── <ST>/                 one folder per state, two-letter postal code (AK ... WY, DC)
        ├── <st>_long_latest.csv          all sources, long format, latest value per week
        ├── <st>_nhsn_wide.csv            hospital admissions, wide format
        ├── <st>_nssp_wide.csv            ED visits, wide format
        ├── <st>_nwss_wide.csv            wastewater, wide format
        ├── <st>_all_sources_wide.csv     one row per week, every source and region side by side
        ├── <st>_census_context.csv       state Census context
        ├── <st>_quality_report.md        coverage, flag counts, consistency checks
        └── sc_long_all_versions.csv.gz   (SC only) full revision history
```

Revision-history files for all 51 jurisdictions (`<st>_long_all_versions.csv.gz`, 2-64 MB each, about 840 MB in total) are attached to each GitHub Release; see [Revision history downloads](#revision-history-downloads).

## Which file should I use?

- **To model or plot one state week by week:** `<st>_all_sources_wide.csv`. One row per week, one column per measure and region, with a `_flag` column next to each value.
- **To work with one source:** `<st>_nhsn_wide.csv`, `<st>_nssp_wide.csv`, or `<st>_nwss_wide.csv`. One row per region (or site) and week.
- **To filter, join, or stack states programmatically:** `<st>_long_latest.csv`. One row per measurement, with full provenance. All states share the same columns, so the files can be concatenated directly.
- **To study data revisions or run a real-time backtest:** `<st>_long_all_versions.csv.gz`, one per state, downloaded from the release (see below).

## Quick start

Python:

```python
import pandas as pd

wide = pd.read_csv("data/SC/sc_all_sources_wide.csv", parse_dates=["observation_week"])
usable = wide["hospital_admission_count_covid_flag"].isin(["observed_valid", "observed_zero"])
covid_admissions = wide.loc[usable, ["observation_week", "hospital_admission_count_covid"]]

# Revision history (SC's copy is in the repo; other states: see below)
# keep_default_na=False keeps category labels as text
history = pd.read_csv("data/SC/sc_long_all_versions.csv.gz", dtype=str, keep_default_na=False)
```

R:

```r
library(readr)
wide <- read_csv("data/SC/sc_all_sources_wide.csv")
history <- read_csv("data/SC/sc_long_all_versions.csv.gz", col_types = cols(.default = "c"))
```

## Revision history downloads

Each state's `<st>_long_all_versions.csv.gz` is attached to the [release](https://github.com/DMA-PRIME/ObsAwareData/releases/tag/v1.1.0%2B2026-08-28). `metadata/release_assets.csv` lists each file's direct download link, size, and SHA-256.

With the [GitHub CLI](https://cli.github.com/):

```bash
# one state
gh release download "v1.1.0+2026-08-28" --repo DMA-PRIME/ObsAwareData --pattern "tx_long_all_versions.csv.gz"
# all states
gh release download "v1.1.0+2026-08-28" --repo DMA-PRIME/ObsAwareData --pattern "*_long_all_versions.csv.gz"
```

Or in Python, from the link in `metadata/release_assets.csv`:

```python
import hashlib, urllib.request
import pandas as pd

assets = pd.read_csv("metadata/release_assets.csv").set_index("state")
a = assets.loc["TX"]
urllib.request.urlretrieve(a["url"], a["file"])
assert hashlib.sha256(open(a["file"], "rb").read()).hexdigest() == a["sha256"]
history = pd.read_csv(a["file"], dtype=str, keep_default_na=False)
```

The larger files expand to several GB in memory when read as text. Read them in chunks (`chunksize=` in pandas), or keep only the columns you need (`usecols=`).

## Before any numeric calculation

Two things to handle:

1. **Filter on the flag, not only on the value.** Filter each value on its `_flag` column (or `observation_state` in the long tables). A blank value with `incidental_missing` is a gap, not a zero.
2. **Drop the Census placeholder code.** A few Census margin-of-error columns hold `-555555555`, the Census Bureau's placeholder for "not applicable". Exclude it from numeric calculations.

## Important caveats

- **Wide tables have no revision history.** They hold only the latest value for each week.
- **ED "regions" are CDC health service areas (HSAs).** These are multi-county units: every county in an HSA shares one reported number.
- **Sites are the only valid geography for wastewater.** A wastewater site can serve several counties, and some serve counties in more than one state.
- **Wastewater activity levels can't be compared across pathogens.** Use `wastewater_activity_category` to compare.
- **The flag thresholds are data-derived, not clinically validated.** See [METHODS.md](METHODS.md) for how they were set, and for the known limitations.

## Versioning

Releases are tagged `v<version>+<data date>`, for example `v1.0.0+2026-08-28`:

- **`<version>`** follows [Semantic Versioning](https://semver.org/) and changes only when the rules for building the data change (structure, processing, or flag rules).
- **`<data date>`** is the release date of the most recent CDC source file used. A data refresh under the same rules keeps the version and changes only the date.

To reproduce an analysis, cite or check out the full tag. [CHANGELOG.md](CHANGELOG.md) lists what changed in each release and each source's release date.

## License and citation

The data are released under the [Creative Commons Attribution 4.0 International License](LICENSE) (CC BY 4.0). The underlying CDC and Census data are public; please also acknowledge the original sources listed in [DATA_SOURCES.md](DATA_SOURCES.md). How to cite this dataset: see [CITATION.cff](CITATION.cff).

This dataset contains only aggregated public surveillance data. It contains no individual-level or protected health information.
