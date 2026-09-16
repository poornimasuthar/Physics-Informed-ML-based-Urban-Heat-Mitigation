# Physics-Informed Explainable ML for Urban Heat Mitigation — Ahmedabad

**ISRO Bharatiya Antariksh Hackathon (BAH) 2026 — Problem Statement 1 (Urban Heat Mitigation)**

A physics-informed, explainable machine learning framework for Surface Urban Heat Island (SUHI) hotspot detection, driver attribution, and cooling-strategy optimization, applied to Ahmedabad, a rapidly urbanizing semi-arid city.

## Overview

The framework combines satellite-derived surface energy balance physics (SEBAL-lite) with an explainable XGBoost regression model to:
1. Predict Land Surface Temperature (LST) at 100 m resolution across Ahmedabad AMC
2. Attribute thermal variability to physical and morphological drivers via SHAP
3. Identify contiguous surface heat hotspots using a composite Heat Stress Index (HSI)
4. Simulate and optimize the spatial placement of cooling interventions (urban greening, cool roofing, water-body expansion)

## Data Sources

| Source | Variables |
|---|---|
| Landsat 8 OLI/TIRS Collection 2 | Land Surface Temperature (April–June 2024) |
| Sentinel-2 | NDVI, NDBI, NDWI, MNDWI, NDMI |
| ESA WorldCover 2021 | Land use / land cover (LULC) |
| ERA5-Land | Air temperature, relative humidity, wind speed |
| OpenStreetMap | Building coverage ratio (BCR), green fraction, water fraction, sky view factor (SVF), street network |
| SEBAL-lite (derived) | Net radiation (Rn), ground heat flux (G), sensible heat (H), latent heat (LE), Bowen ratio, albedo, emissivity |

**Dataset**: 69,312 clean pixels at 100 m resolution, covering Ahmedabad AMC, summer 2024.

## Methodology

1. **`notebooks/01_LST_processing.ipynb`** — Landsat 8 LST retrieval, Sentinel-2 spectral index computation, SEBAL-lite surface energy balance derivation (Rn, G, H, LE, Bowen ratio, albedo).
2. **`notebooks/02_OSM_morphology.ipynb`** — Extraction of urban morphology metrics (building coverage ratio, green/water fraction, sky view factor) from OpenStreetMap at a 39,574-cell grid.
3. **`notebooks/03_ML_modeling.ipynb`** — XGBoost regression (21 features) trained to predict LST, SHAP-based driver attribution, composite Heat Stress Index construction, and scenario-based cooling-intervention simulation and spatial optimization.

## Key Results

- **Model performance**: XGBoost regression, R² = 0.906, RMSE = 0.89 °C (21 predictor variables)
- **LST range**: 31.8–55.2 °C (mean 46.8 °C); mean Bowen ratio 4.6 and mean net radiation 421 W/m², confirming sensible-heat-dominated urban heat island behavior
- **Top SHAP drivers**: surface albedo, net radiation (Rn), NDBI, NDMI, ground heat flux (G)
- **Hotspots**: Composite Heat Stress Index (LST + Bowen ratio) identifies 13,863 hotspot pixels (top 20%), forming an ~83 km² contiguous thermal hotspot in Ahmedabad's dense historic core
- **LULC composition**: Built-up 45.5%, Cropland 34.5%, Tree cover 12.0%, Shrubland 4.1%, Barren 1.6%, Grassland 1.3%, Water 1.1%
- **Urban morphology (OSM)**: 90,908 buildings, 120,929 street segments, 396 green spaces, 224 water bodies; mean building coverage ratio 0.045, mean sky view factor 0.995

### Cooling Intervention Simulation (hotspot zones)

| Intervention | Mean cooling | Max cooling |
|---|---|---|
| Urban greening | 1.54 °C | 6.34 °C |
| Water body expansion | 1.32 °C | 9.64 °C |
| Cool roofing | 0.57 °C | 12.05 °C |
| **Combined** | **4.70 °C** | **24.43 °C** |

Spatial optimization identifies 9,192 priority pixels with cooling potential > 3 °C, guiding ward-level heat mitigation planning.

## Repository Structure

```
notebooks/    Analysis notebooks (LST processing, OSM morphology, ML modeling)
data/         Urban morphology dataset (amd_morphology.csv)
models/       Trained XGBoost model (lst_model_final.pkl)
results/      Text summaries of key findings, SHAP analysis, scenario results
```




