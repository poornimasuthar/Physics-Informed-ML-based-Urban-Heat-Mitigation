# Physics-Informed Explainable ML for Urban Heat Mitigation — Ahmedabad

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

## Key Results - Please refer the .txt files in the results folder. 
| **Model performance** | **LST Range**| **TOP SHAP Drivers**| **Hotspots** | **LULC Composition**| **Urban Morphology (OSM)**|

### Cooling Intervention Simulation (hotspot zones)
Spatial optimization identifies 9,192 priority pixels with cooling potential > 3 °C, guiding ward-level heat mitigation planning.

## Repository Structure
```
notebooks/    Analysis notebooks (LST processing, OSM morphology, ML modeling)
data/         Urban morphology dataset (amd_morphology.csv)
models/       Trained XGBoost model (lst_model_final.pkl)
results/      Text summaries of key findings, SHAP analysis, scenario results
```




