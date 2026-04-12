# 🔥 Kenya Clean Cooking Access Gap Analysis
### A County-Level Geospatial Market Opportunity Study

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat-square)
![GeoPandas](https://img.shields.io/badge/GeoPandas-0.14%2B-green?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)
![Status](https://img.shields.io/badge/Status-Phase%201%20of%202-orange?style=flat-square)
![Data](https://img.shields.io/badge/Data-Simulated%20%E2%80%94%20pipeline%20demo%20only-red?style=flat-square)

> **"Only 31% of Kenyan households use clean cooking — yet electricity access stands at 77%. The infrastructure exists. The market gap is hiding in plain sight."**

This project maps and quantifies Kenya's clean cooking access deficit at county level, identifying the highest-impact intervention zones for distributors, investors, carbon project developers, and policymakers. It is **Phase 1** of a two-phase analysis that will scale to all of Sub-Saharan Africa.

---

## ⚠️ Data Status

The pipeline currently runs on **simulated data** generated to match the structure and schema of the Kenya DHS 2022 Household Recode file. This is intentional at this stage.

| Purpose | Fit? |
|---------|------|
| Testing that pipeline code runs without errors | ✅ Good |
| Checking column names, dtypes, and merges | ✅ Good |
| Visualising output formats and map layouts | ✅ Good |
| Estimating real clean cooking rates | ❌ Not reliable |
| Regression or predictive modelling | ❌ Not reliable |
| County-level policy conclusions | ❌ Not reliable |

**Real data path:** The pipeline is built to ingest the Kenya DHS 2022 Household Recode (HR) file from [dhsprogram.com](https://dhsprogram.com) (free registration). Once that file is substituted into `data/raw/`, all notebooks run unchanged and produce analysis-grade outputs. See `notebooks/01_data_collection.ipynb` for exact download instructions.

---

## 📌 Why This Matters

- **~9.1 million Kenyan households** still rely on charcoal or firewood for cooking
- The Government of Kenya has set a target of **100% clean cooking access by 2028** — four years away
- Access gaps are not uniform: **county-level disparities are large** and drive where interventions deliver the most value
- Carbon project developers, LPG distributors, and impact investors need granular demand intelligence to deploy capital efficiently

---

## 🗺️ What This Project Produces

| Output | Description |
|--------|-------------|
| `outputs/maps/01_access_rate_choropleth.html` | Interactive county-level map of clean cooking access rates |
| `outputs/maps/02_deficit_map.html` | Population-weighted map of households without clean cooking |
| `outputs/maps/03_priority_map.html` | Composite intervention priority score by county |
| `outputs/charts/priority_matrix.html` | High-population × low-access opportunity quadrant chart |
| `outputs/charts/county_clusters.html` | K-means market archetype segmentation |
| `outputs/tables/kenya_county_priority_summary.csv` | All 47 counties ranked by priority score |

---

## 📂 Project Structure

```
kenya-clean-cooking-gap/
│
├── data/                              # ← excluded from Git (see .gitignore)
│   ├── raw/                           # Original downloaded datasets
│   ├── processed/                     # Cleaned, merged county-level dataset
│   └── shapefiles/                    # Kenya county boundaries (GADM)
│
├── notebooks/
│   ├── 01_data_collection.ipynb       # Download & inspect all source data
│   ├── 02_data_processing.ipynb       # Clean, merge, engineer features
│   ├── 03_exploratory_analysis.ipynb  # EDA — distributions, correlations
│   ├── 04_geospatial_maps.ipynb       # Choropleth & deficit maps (Folium)
│   └── 05_priority_analysis.ipynb     # Priority matrix, clustering, CSV export
│
├── outputs/
│   ├── maps/                          # HTML interactive maps
│   ├── charts/                        # Plotly chart exports
│   └── tables/                        # CSV summaries
│
├── docs/
│   └── data_dictionary.md             # Variable definitions and source citations
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 📊 Data Sources

All datasets are **free and publicly available**.

| Dataset | Source | Variables Used |
|---------|--------|----------------|
| Kenya DHS 2022 | [DHS Program](https://dhsprogram.com) | Cooking fuel type, income, gender of HH head by county |
| Kenya National Cooking Transition Strategy 2024 | [energy.go.ke](https://www.energy.go.ke) | County prevalence vs. deficit table |
| World Bank SDG-7 Time Series | [data.worldbank.org](https://data.worldbank.org/indicator/EG.CFT.ACCS.ZS?locations=KE) | National clean cooking access % (2000–2021) |
| Kenya County Shapefiles | [GADM](https://gadm.org/download_country.html) | County geometries |
| Facebook Relative Wealth Index | [data.humdata.org](https://data.humdata.org/dataset/relative-wealth-index) | Sub-national wealth proxy |

> **DHS access note:** Registration is free at dhsprogram.com (approval typically 1–2 days). Request the Kenya 2022 KDHS Household Recode (HR) file. The key variable is `HV226` (type of cooking fuel). Save as `data/raw/KEHR8AFL.csv`.

---

## 🔬 Analytical Framework

### 1. Access Rate Mapping
Clean cooking access rate per county, derived from DHS household fuel data and benchmarked against Kenya's 2028 universal access target.

### 2. Population-Weighted Deficit
```
Deficit (households) = Total HHs × (1 − Clean Cooking Access Rate)
```
Surfaces counties where the *absolute* number of underserved households is largest — the metric that matters for market sizing, not just percentage.

### 3. Priority Matrix (4-Quadrant)
Counties plotted on two axes — total households (market size) vs. access gap — to identify the high-population, high-gap zones that represent the greatest intervention opportunity.

### 4. Affordability vs. Distribution Gap
Overlaying the Facebook Relative Wealth Index against access rates diagnoses whether a county's gap is primarily an **affordability problem** or a **supply/distribution problem** — the two require different interventions.

### 5. K-Means Market Segmentation
Counties clustered into four market archetypes by access rate, urbanisation, population, and wealth — producing actionable segments for distributors and carbon project developers.

---

## 🧪 Hypotheses Tested

1. **Urban ≠ clean** — High urbanisation does not guarantee clean cooking access
2. **The LPG–electricity split** — Counties with high electricity but low LPG penetration signal the e-cooking opportunity
3. **Income threshold** — There is a wealth level above which clean cooking adoption accelerates sharply
4. **Gender disaggregation** — Female-headed households show different fuel choice patterns at the same income level

---

## 🚀 Getting Started

```bash
# Clone the repo
git clone https://github.com/EricNjiraini/kenya-clean-cooking-gap.git
cd kenya-clean-cooking-gap

# Install dependencies
pip install -r requirements.txt

# Launch notebooks
jupyter lab
```

Run notebooks in order: `01 → 02 → 03 → 04 → 05`. Notebook 01 has step-by-step instructions for each dataset download.

---

## 🔭 Phase 2 Preview: Sub-Saharan Africa

This Kenya analysis is the methodological foundation for a broader SSA-wide study that will:
- Apply the same framework across 54 countries using harmonised DHS data
- Integrate OnStove net-benefit rasters (KTH / Nature Sustainability, 2023)
- Rank countries by investment gap: access deficit vs. capital deployed
- Cluster countries into market archetypes for strategic entry analysis

---

## 📖 References

- Kenya National Cooking Transition Strategy, 2024–2028 — Ministry of Energy and Petroleum
- Khavari et al. (2023). "A geospatial approach to understanding clean cooking challenges in sub-Saharan Africa." *Nature Sustainability*
- IEA (2024). *Universal Access to Clean Cooking in Africa*
- DHS Program (2022). *Kenya Demographic and Health Survey*
- WRI (2024). "Leveraging Energy Access Explorer to Advance Kenya's Clean Cooking Agenda"

---

## 👤 Author

**Eric Njiraini** | Data Analytics Professional, Nairobi
*Specialising in business intelligence, Data Analytics, and geospatial analytics in Sub-Saharan Africa*

[![GitHub](https://img.shields.io/badge/GitHub-EricNjiraini-black?style=flat-square&logo=github)](https://github.com/EricNjiraini)

---

*Part of a portfolio series on data analytics in the clean cooking and energy access sector.*
