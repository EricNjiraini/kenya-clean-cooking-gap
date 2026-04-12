# Data Dictionary
## Kenya Clean Cooking Access Gap Analysis

---

### Master Dataset: `kenya_county_clean_cooking.csv / .gpkg`

| Variable | Type | Description | Source |
|----------|------|-------------|--------|
| `county_name` | string | Official county name (47 counties) | KNBS |
| `population_2019` | int | Total population, 2019 Census | KNBS 2019 PHC |
| `total_households_est` | int | Estimated total households (population ÷ 3.9) | Derived |
| `clean_cooking_rate` | float | Share of HH using WHO-clean fuel (0–1) | DHS 2022 |
| `access_gap` | float | 1 − clean_cooking_rate | Derived |
| `hh_without_clean_cooking` | int | Estimated HH without clean cooking | Derived |
| `hh_gap_to_100pct` | int | HH needed to reach 100% access (= deficit) | Derived |
| `priority_score` | float | Composite score: gap size × access rate deficit (0–1) | Derived |
| `urban_rate` | float | Share of HH in urban areas | DHS 2022 |
| `female_headed_rate` | float | Share of HH with female head | DHS 2022 |
| `wealth_index_mean` | float | Mean Facebook Relative Wealth Index | Meta / HDX |
| `wealth_quintile_mode` | int | Most common DHS wealth quintile (1=poorest, 5=richest) | DHS 2022 |
| `sample_hh` | int | DHS sample size for county | DHS 2022 |
| `cluster_label` | string | K-Means market archetype label | Derived |
| `quadrant` | string | 4-quadrant priority matrix label | Derived |
| `geometry` | geometry | County polygon (WGS84 / EPSG:4326) | GADM |

---

### Cooking Fuel Codes (DHS HV226)

| Code | Fuel | WHO Classification |
|------|------|--------------------|
| 1 | Electricity | ✅ Clean |
| 2 | LPG / Natural gas | ✅ Clean |
| 3 | Biogas | ✅ Clean |
| 4 | Kerosene | ❌ Polluting |
| 5 | Coal / Lignite | ❌ Polluting |
| 6 | Charcoal | ❌ Polluting |
| 7 | Wood | ❌ Polluting |
| 8 | Straw / Shrubs / Grass | ❌ Polluting |
| 9 | Agricultural crop | ❌ Polluting |
| 10 | Animal dung | ❌ Polluting |
| 96 | Other | ❌ Polluting |

---

### Priority Score Formula

```
priority_score = 
    (hh_without_clean_cooking / max(hh_without_clean_cooking)) 
  × ((1 − clean_cooking_rate) / max(1 − clean_cooking_rate))
```

Range: 0 (lowest priority) to 1 (highest priority)  
Interpretation: A county scores high when it has BOTH a large absolute deficit AND a large percentage gap. A densely populated county with moderate access will score differently from a sparsely populated county with very low access — this is intentional.

---

### Sources & Citations

- **Kenya DHS 2022**: Kenya National Bureau of Statistics and ICF. *2022 Kenya Demographic and Health Survey*. Nairobi, Kenya, and Rockville, Maryland, USA: KNBS and ICF. Available at: dhsprogram.com
- **KNCTS 2024**: Government of Kenya. *Kenya National Cooking Transition Strategy 2024–2028*. Ministry of Energy and Petroleum.
- **GADM**: Global Administrative Areas. University of California, Davis. gadm.org
- **World Bank SDG-7**: IEA, IRENA, UNSD, World Bank, WHO. (2023). *Tracking SDG 7: The Energy Progress Report.* Indicator EG.CFT.ACCS.ZS
- **Facebook RWI**: Chi, G., et al. (2022). "Microestimates of wealth for all low- and middle-income countries." *PNAS*. Data via HDX.
