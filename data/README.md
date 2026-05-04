# Data folder

This folder contains the spatial, tabular, and model-output datasets used in the regional and local-scale lake ice phenology analyses for the `landcover-lake-ice-project`.

## Brief file descriptions

- `hex_shp/`: Spatial shapefile for the 150 km hexagonal grid used to define regional analysis units.
- `hex_stats.csv`: Hexagon-level landscape and anthropogenic-pressure summaries used for PCA, clustering, and regional interpretation.
- `ice_phenology_all.csv`: Lake-level annual ice-on and ice-off phenology records used for regional lake ice analysis.  
  > 🚨 **Note:** <span style="color:red">This file will be shared publicly soon.</span>
- `ice_dur_ml.csv`: Lake-year modeling dataset used to predict ice duration from meteorological, land-cover, and morphometric predictors.
  > 🚨 **Note:** <span style="color:red">This file will be shared publicly soon.</span>
- `model/`: Saved random forest model outputs, variable importance results, and partial dependence data used to reproduce local-scale modeling figures.

The datasets support two main parts of the analysis:

1. **Regional-scale analysis** — summarizes lake ice phenology and landscape characteristics across 150 km hexagonal spatial regions.
2. **Local-scale modeling** — uses lake-level meteorological, land-cover, and morphometric predictors to model lake ice duration using random forest regression.

## Folder structure

```text
data/
├── hex_shp/
│   ├── hex_150km.dbf
│   ├── hex_150km.prj
│   ├── hex_150km.shp
│   └── hex_150km.shx
├── model/
│   ├── pd_cloud_dur.rds
│   ├── pd_depth_dur.rds
│   ├── pd_dev_dur.rds
│   ├── pd_fr_dur.rds
│   ├── pd_pc_dur.rds
│   ├── pd_precip_dur.rds
│   ├── pd_shore_dur.rds
│   ├── pd_tave_dur.rds
│   ├── pd_vol_dur.rds
│   ├── rf_dur_model.rds
│   ├── vi_grouped.rds
│   └── vi_indiv.rds
├── hex_stats.csv
├── ice_dur_ml.csv
├── ice_phenology_all.csv
└── README.md
```

## Dataset descriptions

| File or folder | Description | Main use in analysis |
|---|---|---|
| `hex_shp/` | Shapefile components for the 150 km hexagonal spatial grid covering the study region. The shapefile is used to represent regional analysis units and to assign lakes to spatial clusters based on location. | Used in the regional-scale analysis to map hexagonal regions, overlay lake locations, and join lake ice phenology records to spatial clusters. |
| `hex_stats.csv` | Hexagon-level summary dataset containing land-cover and anthropogenic-pressure variables for each 150 km spatial block. Key variables used in the analysis include `hex_id`, `Developed_mean`, `Forest_mean`, `Planted_Cultivated_mean`, `night_light_mean`, `total_waste_discharged_m3_d`, `footprint_mean`, `influance_mean`, `population_mean`, `nonrenewable_total_capacity_mw`, `road_density_mean`, and `renewable_total_capacity_mw`. | Used for PCA, k-means clustering, radar plots, and regional characterization of human influence, land cover, infrastructure, and population gradients. |
| `ice_phenology_all.csv` | Lake-level ice phenology dataset containing annual ice-on and ice-off records for lakes in the study area. Variables used in the code include `lake_id`, `year`, `lat`, `lon`, `ice_on_date`, `ice_on_doy`, `ice_off_date`, and `ice_off_doy`. | Used to calculate lake-level ice-on and ice-off variability, impute missing phenology values, estimate Sen’s slopes, and compare ice phenology metrics across regional clusters. |
| `ice_dur_ml.csv` | Lake-year modeling dataset for local-scale ice duration analysis. It contains the response variable `ice_dur`, lake identifiers, coordinates, year, and local-scale predictors. Predictors used in the random forest model include meteorological variables (`tave`, `precip`, `cloud`), land-cover variables (`Developed`, `Planted_Cultivated`, `Forest`), and lake morphometric variables (`lake_area_km2`, `shore_len`, `lake_shorelinedevfactor`). In the script, `lake_shorelinedevfactor` is renamed to `Shore_dev`, and `lake_area_km2` is renamed to `lake_area`. | Used to train and evaluate the random forest model for lake ice duration with spatio-temporal cross-validation. Also used to generate variable importance and partial dependence analyses. |
| `model/` | Folder containing saved R objects generated from the local-scale random forest analysis. These files allow the model, variable importance results, and partial dependence objects to be loaded without rerunning the full modeling workflow. | Used to reproduce model-performance plots, grouped and individual variable importance plots, and partial dependence plots for meteorological, land-cover, and morphometric predictors. |

## Model output files

| File | Description |
|---|---|
| `rf_dur_model.rds` | Saved tuned random forest model for predicting lake ice duration. |
| `vi_indiv.rds` | Individual-variable permutation importance results. |
| `vi_grouped.rds` | Grouped permutation importance results for predictor groups such as meteorology, land cover, and lake morphology. |
| `pd_dev_dur.rds` | Partial dependence results for developed land cover. |
| `pd_pc_dur.rds` | Partial dependence results for planted/cultivated land cover. |
| `pd_fr_dur.rds` | Partial dependence results for forest land cover. |
| `pd_tave_dur.rds` | Partial dependence results for average temperature. |
| `pd_precip_dur.rds` | Partial dependence results for precipitation. |
| `pd_cloud_dur.rds` | Partial dependence results for cloud cover. |
| `pd_depth_dur.rds` | Partial dependence results for shoreline length. |
| `pd_shore_dur.rds` | Partial dependence results for shoreline development factor. |
| `pd_vol_dur.rds` | Partial dependence results for lake area. |

## Notes

- The `hex_shp/` shapefile must be kept as a complete set of shapefile components (`.shp`, `.shx`, `.dbf`, `.prj`) for spatial reading with `sf::read_sf()`.
- The CSV files are read relative to the project root using `here::here()`.
- The `model/` files are derived outputs from the local-scale random forest workflow. They are provided to make the analysis faster to reproduce without rerunning the full model tuning, variable importance, and partial dependence calculations.
- Column descriptions above are based on the variables used directly in the rendered Quarto analysis script.