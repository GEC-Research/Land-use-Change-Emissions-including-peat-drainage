# Land-Use-Change (LUC) Emissions from Animal Feed & Pasture (2018--2022)

This repository reproduces the analysis of **consumption-driven
land-use-change (LUC) emissions** associated with:

-   **Feed crops:** soybeans, rapeseed, sunflower seed, maize, barley,
    sorghum
-   **Pasture expansion:** ruminant-driven grazing land expansion

The workflow integrates two primary datasets:

1.  **FAOSTAT Crops & Livestock (SCL)** feed-use data (2018--2022)
2.  **Singh et al. (2024)** hybrid trade-flow LUC dataset (DeDuCE v2.0)

All processing and figure generation are implemented in:

`LUC_Emissions_2018-2022.ipynb`

------------------------------------------------------------------------

## 1. Repository structure

    .
    ├── data/
    │   ├── FAOSTAT_crops_feed_data.csv
    │   └── Singh et al 2024 - Commodity-driven deforestation, carbon emissions & trade 2018-2022.xlsx
    ├── outputs/
    │   ├── flows_feed_only_LUC_2018_2022.csv
    │   ├── flows_feed_pasture_total_LUC_2018_2022.csv
    │   ├── Fig_feed_pasture_total_LUC_flows_2018_2022.pdf
    │   └── Fig_feed_pasture_total_LUC_flows_2018_2022.png
    └── LUC_Emissions_2018-2022.ipynb

------------------------------------------------------------------------

## 2. Input Data (Manual Download Required)

Both datasets must be downloaded manually to ensure full
reproducibility.

------------------------------------------------------------------------

## 2.1 FAOSTAT Crops & Livestock Products (SCL)

**Official portal:**\
https://www.fao.org/faostat/en/#data/SCL

### Download Instructions

1.  Select **Domain**: Crops and Livestock Products (SCL)

2.  Select **Years**: 2018--2022

3.  Select **All Countries**

4.  Select **Elements (use categories)** --- select ONLY:

    -   Food
    -   Feed
    -   Seed
    -   Processing
    -   Loss
    -   Other uses (non-food)
    -   Residuals

    Do NOT select: Production, Yield, Imports, Exports, Stock variation.

5.  Select **Items (crops and oilseed cakes)**:

    **Seed crops:**

    -   Soybeans
    -   Rapeseed
    -   Sunflower seed
    -   Maize (corn)
    -   Barley
    -   Sorghum

    **Oilseed cakes (animal feed products):**

    -   Cake of soybeans
    -   Cake of rapeseed
    -   Cake of sunflower seed

6.  Download data as **CSV**

7.  Save locally as:

    data/FAOSTAT_crops_feed_data.csv

### Purpose in Analysis

FAOSTAT is used **only to compute global feed-use shares**, defined as:

    Feed Share = Feed Use / Total Domestic Use

where:

    Total Domestic Use = Food + Feed + Seed + Processing + Loss + Other uses + Residuals

For oilseeds, feed is reported at the cake level and converted to
seed-equivalent feed using fixed crushing yields:

-   Soybeans: 0.80
-   Rapeseed: 0.61
-   Sunflower seed: 0.59

FAOSTAT trade data are not used.

------------------------------------------------------------------------

## 2.2 Singh et al. (2024) --- Commodity-Driven Deforestation & Trade (DeDuCE v2.0)

**Official dataset (Version 2.0):**\
https://zenodo.org/records/10633818

### Download Instructions

1.  Download the Excel file:

    Singh et al 2024 - Commodity-driven deforestation, carbon emissions & trade 2001–2022.xlsx

2.  Retain only the worksheet:

    Trade flows–hybrid

3.  Filter rows for the years:

    2018–2022

4.  Save locally as:

    data/Singh et al 2024 - Commodity-driven deforestation, carbon emissions & trade 2018–2022.xlsx

### Purpose in Analysis

Singh et al. (2024) provides:

-   Bilateral **producer → consumer trade flows**
-   Commodity-level **land-use-change CO2 emissions**
-   Units: **Mt CO2**
-   Includes **deforestation + peatland emissions**

Only the following commodities are retained:

-   **Feed crops:** soybeans, maize, barley, sorghum, rapeseed,
    sunflower seed
-   **Pasture-based products:** ruminant meat (cattle, bovine, beef)

All other commodities are excluded.

------------------------------------------------------------------------

## 3. Region Groups (GN, CN, GS)

Countries are mapped into:

-   **Global North (GN)**
-   **China (CN)**
-   **Global South excluding China (GS)**

Final results are reported for flows:

-   GN → GS
-   CN → GS
-   GS → GN

------------------------------------------------------------------------

## 4. Method Summary

1.  Load bilateral land-use-change (LUC) emissions from the Singh et
    al. (2024) hybrid trade-flow dataset.

2.  Filter data to the years 2018--2022.

3.  Retain only commodities linked to animal farming:

    -   Feed crops: soybeans, maize, barley, sorghum, rapeseed,
        sunflower seed
    -   Pasture-based products: ruminant meat (cattle, bovine, beef)

4.  Load FAOSTAT SCL domestic-use data for the same crops and years.

5.  Compute global feed-use shares as:

    Feed Share = Feed Use / Total Domestic Use

6.  Convert oilseed cake feed into seed-equivalent feed using fixed
    crushing yields:

    -   Soybeans: 0.80
    -   Rapeseed: 0.61
    -   Sunflower seed: 0.59

7.  Apply feed shares to Singh crop-related LUC emissions.

8.  Attribute 100% of ruminant-meat LUC emissions directly to pasture.

9.  Combine feed-driven and pasture-driven LUC.

10. Map producer and consumer countries into GN, CN, and GS.

11. Aggregate results to directional trade flows:

    -   GN → GS
    -   CN → GS
    -   GS → GN

12. Export final CSV tables and LUC flow figures.

------------------------------------------------------------------------

## 5. Running the Notebook

### Requirements

-   Python ≥ 3.10
-   pandas
-   numpy
-   matplotlib
-   openpyxl

### Install

    pip install pandas numpy matplotlib openpyxl

### Run

    jupyter notebook LUC_Emissions_2018-2022.ipynb

------------------------------------------------------------------------

## 6. Data Sources

**Singh et al. (2024):**
Commodity-driven deforestation, associated carbon emissions and trade
2001--2022 (Version 2.0).
https://zenodo.org/records/10633818

**FAOSTAT:**
FAOSTAT Crops and Livestock Products (SCL).
https://www.fao.org/faostat/en/#data/SCL

------------------------------------------------------------------------

## License

- **Code:**  
  MIT License.

- **Data:**  
  This repository uses third-party datasets that are subject to their own licenses and terms of use, including FAOSTAT data and the commodity-driven deforestation and emissions dataset by Singh et al. (2024).  
  Users should consult the original data providers for full licensing details.

------------------------------------------------------------------------
