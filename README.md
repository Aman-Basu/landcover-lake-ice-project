# landcover-lake-ice-project
This repository contains Quarto-based R code and supporting data for the article "Elucidating the extent of the influence of land cover on ice phenology across lakes in the northern contiguous United States: Implications for ecosystem management"

[![DOI](https://zenodo.org/badge/DOI/XX.XXXX/zenodo.XXXXXXX.svg)](https://doi.org/XX.XXXX/zenodo.XXXXXXX)


🌐 **Rendered HTML report:**  
[View the Quarto report](https://aman-basu.github.io/landcover-lake-ice-project/scripts/index.html)

## Project overview

Lake ice phenology is influenced by climate, lake morphology, and surrounding landscape conditions. This project examines how regional landscape patterns and local-scale drivers relate to lake ice timing and duration.

The analysis includes:

- Regional-scale summaries of lake ice phenology and land-cover characteristics
- Spatial analysis using hexagonal regions
- Data wrangling and visualization of ice phenology records
- Local-scale modeling of lake ice duration
- Machine-learning-based assessment of important predictors

## Repository structure

```text
landcover-lake-ice-project/
├── data/
│   ├── hex_shp/                  # Hexagonal spatial region files
│   ├── model/                    # Model-related data or outputs
│   ├── hex_stats.csv             # Regional hex-level summary data
│   ├── ice_dur_ml.csv            # Ice duration modeling dataset
│   ├── ice_phenology_all.csv     # Lake ice phenology records
│   └── README.md
├── docs/
│   ├── scripts/
│   │   └── index.html            # Rendered Quarto HTML report
│   ├── site_libs/                # Quarto-generated website assets
│   └── search.json
├── scripts/
│   ├── index.qmd                 # Main Quarto analysis document
│   └── rosm.cache/               # Local map tile/cache folder
├── _quarto.yml                   # Quarto project configuration
├── .gitignore
├── LICENSE
└── README.md