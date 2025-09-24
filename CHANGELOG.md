
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
