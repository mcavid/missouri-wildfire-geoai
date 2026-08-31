# Data

The raw and intermediate geospatial datasets used in this project are not included in this repository because of file size, licensing, and reproducibility considerations.

## Primary data sources

| Dataset | Source | Role |
|---|---|---|
| Wildfire occurrences (1992–2020) | USDA Forest Service, Fire Program Analysis Fire-Occurrence Database (FPA-FOD) | Historical wildfire occurrence and target construction |
| Land cover (2021) | National Land Cover Database (NLCD) | Forest, grassland, agriculture, and other land-cover predictors |
| Climate normals (1991–2020) | PRISM Climate Group | Precipitation, mean temperature, maximum temperature, and vapor pressure deficit |
| Elevation | Missouri Spatial Data Information Service (MSDIS) | Terrain predictor |
| Population and WUI exposure | SILVIS Lab | Population density and wildland–urban interface exposure |
| Roads and railroads | Missouri Department of Transportation (MoDOT) | Infrastructure and accessibility predictors |
| Social Vulnerability Index (2022) | CDC/ATSDR | Community vulnerability component |
| Missouri boundary | Missouri Department of Agriculture | Study-area boundary |

## Exploratory data sources

The exploratory feature-analysis notebook additionally investigates:

- LANDFIRE fuel characteristics (2024)
- gSSURGO soil properties (2025)
- TerraClimate wind and drought variables (2015–2024)
- Terrain and railroad-proximity variables

## Processed project data

The notebooks expect local project geodatabases such as:

```text
data/
├── final_tables.gdb/
└── New_Wildfire_Finished.gdb/
```

These geodatabases are intentionally excluded from version control.

Most source datasets were clipped to Missouri, projected to a common coordinate reference system, and summarized to a statewide 5 km × 5 km grid before modeling.

The primary modeling workflow uses `Cell_ID_Stable` as the common merge key across geospatial layers.

## Reproducing the analysis

1. Download the required source datasets from their official providers.
2. Prepare the geospatial layers using the workflow documented in the project report.
3. Place the processed geodatabases in the local `data/` directory.
4. Run `notebooks/01_primary_wildfire_model.ipynb`.
5. Use `notebooks/02_exploratory_feature_analysis.ipynb` for the extended exploratory analysis.

The primary final model uses a binary wildfire-susceptibility target:

- **0:** 0–3 historical fires per grid cell
- **1:** 4 or more historical fires per grid cell

The second notebook is exploratory and evaluates an expanded predictor set and alternative modeling choices.
