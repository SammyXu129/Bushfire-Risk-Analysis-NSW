# Bushfire Risk Analysis

## Introduction

This repository contains the code and data for a comprehensive bushfire risk analysis conducted on regions in New South Wales (NSW), focusing primarily on Greater Sydney. The analysis involves computing bush risk scores for neighborhoods based on various leading factors and explores the impact of bushfire risk on neighborhood affluence.

## Dataset Description

### Datasets

1. **Neighborhoods.csv**
   - Source: Australian Bureau of Statistics (ABS)
   - Information: Population, number of dwellings, income, rental, etc.
   - Key Identifier: `area_id`

2. **StatisticalAreas.csv**
   - Source: Australian ABS
   - Information: Geographically hierarchical regions
   - Key Identifiers: `area_id`, `parent_id`

3. **BusinessStats.csv**
   - Source: ABS
   - Information: Overall business count, counts of different business categories
   - Key Identifier: `area_id`

4. **RFSNSW.shp**
   - Source: NSW Rural Fire Service
   - Information: Locations and characteristics of vegetation categories
   - Key Identifier: Spatial information (`geom`)

5. **SA2_2016_AUST.shp**
   - Source: ABS
   - Information: Geographic information of NSW regions
   - Key Identifier: Spatial information (`geom`)

6. **NSW_Wetlands_2016.shp**
   - Source: data.gov.au
   - Information: Wetland and non-wetland details
   - Key Identifier: Spatial information (`geom`)

### Data Pre-processing

1. **Data Wrangling**
   - Remove null values and duplicates.
   - Standardize column names to lowercase.
   - Convert numeric columns (e.g., population, number of dwellings) to integer format.

2. **Data Integration**
   - Merge datasets for enhanced analysis.
   - Use spatial joins to integrate geographic information.

3. **Schema Setup**
   - Utilize PostgreSQL server at the University of Sydney.
   - Establish tables with primary and foreign keys for effective data management.

## Fire Risk Score Analysis

### Calculation Explanation

We calculate the fire risk score for each neighborhood using the following formula:

\[ \text{Fire Risk Score} = S(z_{population} + z_{dwelling} + z_{business} + z_{bfpl} - z_{assistive\_service} - z_{wetland}) \]

- \( S \): Logistical function (sigmoid function)
- \( z \): Z-score (standard score) of a measure

### Density Calculations

1. **Population Density**
   - Divide population per region by corresponding land area.

2. **Dwelling Density**
   - Divide dwelling per region by corresponding land area.

3. **Business Density**
   - Merge neighborhood and business datasets and calculate business density.

4. **Assistive Service Density**
   - Calculate density based on "health_care_and_social_assistance" and "public_administration_and_safety."

5. **BFPL Density**
   - Adjust land area of vegetation plots based on risk parameters.
   - Sum up overall vegetation area per neighborhood and divide by corresponding land area.

6. **Wetland Density**
   - Map wetland locations into neighborhoods.
   - Calculate total overlapped wetland area per region and determine wetland density.

### Result Description

- **Boxplot (Plot 1)**
  - Majority of scores cluster around 0.3 to 0.6, indicating moderate to low risk.

- **Maps (Map 2 and Map 3)**
  - Outline spread of risk scores for neighborhoods across Greater Sydney.
  - Higher risk in inner and North parts, rural areas more prone to bushfires.

## Correlation Analysis

- **Risk Score vs. Median Annual Income**
  - Positive trend but weak association.
  - Potential influence from various factors; further research needed.

- **Risk Score vs. Monthly Rent**
  - Negative trend but weak association.
  - Statistical insignificance, requires further investigation.
