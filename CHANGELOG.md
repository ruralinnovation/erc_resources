
## Economic Development Tool data refresh — June 2026

### Added

- **Updated data** 
  All data source vintages reviewed against the [CORI Data Release Calendar (June 8, 2026)](docs/data-release-calendar.html):
  - Broadband coverage and access metrics updated to FCC National Broadband Map Version 8 (December 2025 data)
  - Population metrics updated to Census PEP 2025 covering 2010-2025
  - Wage and salary employment and compensation QCEW covering 2010-2025
  - Business formation metrics updated to BFS 2025 covering 2010-2025
  - Building permits metric updated to BFS 2025 covering 2010-2025
 Private capital access metrics Form D, 5-year window shifted to 2021-2025


### Schema Migration

Pipeline fully migrated from `proj_erc` to `proj_econ_dev_tool` PostgreSQL schema.

### Technical Notes

  Updates in `params.yml`:
  - `acs.latest_year`: `[2023]` → `[2024]`; paired comparison year shifts from 2018 to 2019
    (`n_year_change_basis = 5`). Previously postponed in the December 2025 release.
  - `gen_bea` table years extended to include 2024 (`CAINC1` population, `CAGDP1` real GDP;
    full range now 2010–2024). Note: `load_bea.R` is non-functional (requires `BEA_API_KEY`
    and `doctR` package); 2024 row copied from `proj_erc` snapshot.
  - `fcc.nbm_release`: `nbm_block-J25` → `nbm_block-D25` (FCC NBM Version 8, December 2025)
  - `pep.latest_year`: `[2024]` → `[2025]`; county totals released March 26, 2026;
    sourced via `cori.data.pep` S3 package
  - `qcew.latest_year`: `[2024]` → `[2025]`; Q4 2025 + Preliminary Annual 2025 released
    June 2, 2026; direct BLS download via `qcew_utils.R`
  - `bps.latest_year`: `[2024]` → `[2025]`; vintage 2025 captured June 3, 2026;
    sourced via `cori.data.bps` S3 package
  - `formd.base_year`: `[2020]` → `[2021]`; `formd.latest_year`: `[2024]` → `[2025]`;
    5-year window now covers 2021–2025
  - `bfs.latest_year`: `[2024]` → `[2025]`; held pending schema review in prior release;
    BFS 2022 NAICS compatibility with existing pipeline confirmed
  - `bds.latest_year`: held at `[2023]`; 2024 BDS vintage not expected until approximately
  September 2026
- `assemble_data.R` Google Sheets dependencies replaced with local CSV reads:
  `data/codebook.csv`, `data/metrics.csv`, `data/research_language.csv`, `data/key_stats.csv`
- PatentsView S3 path returns 403 Forbidden; `patents_tidy` copied from `proj_erc` snapshot
  pending investigation of the PatentsView data access policy change
- Pitchbook source table `venture_capital.pitchbook_company_geocoded_addresses` absent from
  database; `pitchbook_tidy` copied from `proj_erc` snapshot
- `load_bea.R` requires `BEA_API_KEY` environment variable (not present in current
  environment); `bea_tidy` copied from `proj_erc` snapshot

---

## ERC Tool V3 Updates - January 2025

### Added

- **Updated data**:
  - ACS 2024; 5-year comparison window shifts from 2018–2023 to 2019–2024
  - BEA GDP and income series extended through 2024
  - Broadband coverage and access metrics updated to FCC National Broadband Map (June 2025 data)

## ERC Tool V3 Updates - December 2025

### Added

- **Updated data**
  - Source population stats from Population Estimates Program (formerly sourced from BEA)
  - Source employment stats from QCEW (formerly source from BEA)
  - Connecticut now includes planning regions and historic counties
  - All other data updated to latest releases (except for ACS/FormD; postponed)


## ERC Tool V3 Updates - June 2025

### Added

- **New Quality of Life category** including:
  - Quality of Life percentile over time metric
  - Housing-related indicators

- **New Entrepreneurship metric**: Number of startups in each county or region (sourced from PitchBook)

- **Introduction section enhancements**:
  - Nonmetro status for each county
  - Population data for each county

- **Update to broadband metrics**: FCC NBM data release update

#### Technical notes

- **Average compensation per worker** and **Employment** metrics have been updated due to the discontinuation of regional data tables from the Bureau of Economic Analysis (result of federal budget cuts)
  - These metrics are now sourced from the Bureau of Labor Statistics' *Quarterly Census of Employment and Wages* (QCEW)
  - Using **Average annual pay** and **Average annual employment** data

- Refined the language, metrics, and ETL processes associated with the Form D dataset following insights from the report *Rural America's Struggle to Access Private Capital*

- Reorganized the grouping and order of metrics within the tool based on feedback from Research Director Dr. Amanda Weinstein

- Revised the names of urbanization level categories for improved clarity and consistency

- **Broadband service data updated** with the December 2024 release of the FCC National Broadband Map
  - FCC NBM data now includes satellite service coverage, affecting BSL calculations and rural broadband metrics
    - Integration of satellite service availability has significant impact on total Broadband Serviceable Locations (BSLs)
  - Updated data reflects biannual NBM release cycle with improved coverage metrics
