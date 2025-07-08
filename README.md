# mapdata_fips_aggregation
selenium, chrome_webdriver, BS4<br>
FIPS scraping<br>
Choropleth shapefile pairing<br>
alternate geocoding (public api)<br>

## Main Features & Purpose

This repository is a **geospatial data processing pipeline** that combines multiple data sources and geocoding methods to enrich address data with FIPS (Federal Information Processing Standards) codes for mapping and choropleth visualization.

### Core Components

#### 1. **Selenium-Based FIPS Code Scraping** (`selenium_fips/`)
- **Web scraping automation** using Selenium WebDriver with Chrome/Brave browser
- Targets the **US Census Bureau's geocoding service** (`https://geocoding.geo.census.gov/geocoder/geographies/coordinates?form`)
- **Coordinate-to-FIPS conversion**: Takes latitude/longitude coordinates and retrieves corresponding FIPS codes
- **State-specific processing**: Separate notebooks for each state 
- **Error handling**: Manages timeouts, missing data, and multiple FIPS returns
- **Data cleaning**: Removes brackets, handles empty results, processes regex patterns

#### 2. **Google Geocoding API Integration** (`google_geocoder/`)
- **Address geocoding** using Google Maps Geocoding API
- Converts physical addresses to latitude/longitude coordinates
- **Batch processing** with progress tracking (tqdm)
- **Error handling** for addresses not found
- **API key management** for Google services

#### 3. **Data Pipeline Architecture**
The workflow follows this pattern:
```
Raw Address Data → Google Geocoding → Lat/Long Coordinates → Census FIPS Scraping → Enriched Dataset
```

### Key Technical Features

#### **Multi-Source Data Integration**
- Combines Google's geocoding accuracy with Census Bureau's authoritative FIPS data
- **Fallback mechanisms**: Uses existing FIPS data when available, fills gaps with scraped data
- **Data validation**: Filters for valid coordinates and handles null values

#### **State-by-State Processing**
- Modular approach with separate processing for each US state
- **Scalable architecture** for handling large datasets across multiple states
- State-specific FIPS code validation (e.g., NY codes starting with "36")

#### **Robust Error Handling**
- Manages web scraping timeouts and connection issues
- Handles missing geocoding results
- **Data quality checks**: Validates coordinate ranges and FIPS code formats

#### **Data Merging & Enrichment**
- **Pandas-based data manipulation** for joining datasets
- Preserves original data while adding new FIPS information
- **Column management**: Handles duplicate columns and data type conversions

### Use Cases & Applications

#### **Choropleth Mapping**
- Enables creation of color-coded maps based on geographic regions
- FIPS codes provide standardized geographic boundaries for visualization

#### **Geographic Data Analysis**
- Supports analysis of loan data, demographic information, or other location-based datasets
- Enables aggregation by census tracts, counties, or other geographic units

#### **Data Standardization**
- Converts inconsistent address formats into standardized geographic identifiers
- Creates linkages between different geographic datasets

### Technical Stack
- **Python Libraries**: pandas, selenium, requests, BeautifulSoup, tqdm
- **Web Technologies**: Chrome WebDriver, Google Maps API
- **Data Sources**: US Census Bureau, Google Geocoding Service
- **Output Format**: CSV files with enriched geographic data

### Repository Structure Benefits
- **Modular design** allows for easy state-by-state processing
- **Jupyter notebooks** provide interactive development and debugging
- **Separation of concerns** between geocoding and FIPS retrieval
- **Reusable components** across different geographic regions

This repository essentially serves as a **comprehensive geocoding and geographic enrichment pipeline** that transforms raw address data into map-ready datasets with standardized FIPS codes, making it valuable for any application requiring US geographic data visualization or analysis.
