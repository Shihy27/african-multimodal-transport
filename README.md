# Uneven multimodal transport expansion reshapes regional economic divergence in Africa

This repository contains the Python notebooks used for the analyses in *Uneven multimodal transport expansion reshapes regional economic divergence in Africa*. The study evaluates associations between the expansion of roads, paved highways, railways, railway stations, ports and aeroways and economic growth, sectoral development, welfare and wealth inequality across African countries from 2015 to 2024.

## Repository contents


| Notebook                                            | Purpose                                                                                          |
| ----------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `01_process_osm_infrastructure.ipynb`               | Extract transport infrastructure layers from OpenStreetMap PBF snapshots.                        |
| `02_clip_infrastructure_to_africa_arcpy.ipynb`      | Clip annual infrastructure layers to the African study area (ArcPy).                             |
| `03_project_infrastructure_layers_arcpy.ipynb`      | Project infrastructure layers and calculate length/area attributes (ArcPy).                      |
| `04_project_administrative_boundaries_arcpy.ipynb`  | Project administrative boundaries and calculate areas (ArcPy).                                   |
| `05_process_wealth_inequality_data.ipynb`           | Harmonize World Inequality Database records and construct wealth-distribution indicators.        |
| `06_psm_did_railway_impact.ipynb`                   | Estimate the Addis Ababa-Djibouti railway effect using PSM-DID and event-study checks.           |
| `07_system_gmm_robustness_checks.ipynb`             | Run dynamic-panel system-GMM robustness analyses.                                                |
| `08_multimodal_transport_economic_divergence.ipynb` | Produce the main analysis of infrastructure expansion and regional economic divergence.          |
| `09_mode_specific_sectoral_effects.ipynb`           | Evaluate transport-mode-specific associations with sectoral development.                         |
| `10_multiscale_transport_economic_effects.ipynb`    | Evaluate temporal and scale-dependent heterogeneity in transport-economic associations.          |
| `11_transport_welfare_and_inequality.ipynb`         | Evaluate welfare translation, inequality mitigation and scale-adjusted infrastructure residuals. |

## Software requirements

The analyses were developed with Python 3.11.3. Create an isolated environment and install the public Python dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

The preprocessing notebooks `02`--`04` require ArcPy and therefore an active ArcGIS Pro installation. ArcPy is proprietary and is intentionally not included in `requirements.txt`. Run notebooks `01` and `05`--`11` in the Python environment above; run notebooks `02`--`04` with the Python environment supplied by ArcGIS Pro.

## Data sources

The repository contains code only. Download data from the original providers and comply with their current terms of use before running the notebooks.


| Dataset                       | Use in this study                                                                                          | Source                                                                            |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| OpenStreetMap Africa extracts | Roads, paved highways, railways, railway stations, ports and aeroways                                      | [Geofabrik](https://download.geofabrik.de/africa.html)                            |
| Administrative boundaries     | Country and subregion spatial layers                                                                       | [Natural Earth](https://www.naturalearthdata.com/)                                |
| African macroeconomic data    | GDP, GDP per capita, population, exchange rates, price indices and household final consumption expenditure | [African Development Bank data portal](https://dataportal.opendataforafrica.org/) |
| Sectoral value added          | Agriculture, industry and services                                                                         | [World Bank Open Data](https://data.worldbank.org/)                               |
| Wealth-distribution data      | Top 1%, top 10% and bottom 50% wealth shares                                                               | [World Inequality Database](https://wid.world/world/)                             |

## Configuration and execution

The notebooks use English-only local paths. Its layout is:

```text
E:\Africa_Infrastructure_Data\
├── infrastructure\
├── boundaries\
├── boundaries_project\
├── boundaries_project_49\
├── wid\
├── afdb\
├── world_bank\
├── transport_statistics_2015_2025.xlsx
└── wealth_inequality_2015_2024.xlsx
```

On another computer, create the same directory layout (or update the path variables near the top of each notebook) and place the downloaded data in the corresponding locations. Figure and table products are written to the repository-relative `outputs/` directory.

Run the notebooks in this order:

1. `01_process_osm_infrastructure.ipynb`
2. `02_clip_infrastructure_to_africa_arcpy.ipynb`
3. `03_project_infrastructure_layers_arcpy.ipynb`
4. `04_project_administrative_boundaries_arcpy.ipynb`
5. `05_process_wealth_inequality_data.ipynb`
6. `06_psm_did_railway_impact.ipynb`
7. `07_system_gmm_robustness_checks.ipynb`
8. `08_multimodal_transport_economic_divergence.ipynb`
9. `09_mode_specific_sectoral_effects.ipynb`
10. `10_multiscale_transport_economic_effects.ipynb`
11. `11_transport_welfare_and_inequality.ipynb`

Execute each notebook from top to bottom. Historical notebook outputs have been removed intentionally so that figures, tables and diagnostics are regenerated in the local environment. The analysis notebooks use the processed country-year infrastructure table produced by the preprocessing workflow together with the external socioeconomic data listed above.

## Reproducibility notes

- Keep raw data outside version control. The supplied `.gitignore` excludes common large geospatial and tabular formats.
- Use the same input extracts, country-name harmonization and analysis period to reproduce the reported estimates.
- The model notebooks implement system-GMM, PSM-DID/event-study and multiscale analyses described in the manuscript Methods and Supplementary Information.

## Code availability and citation

Please cite the associated manuscript when using or adapting this code:

> *Uneven multimodal transport expansion reshapes regional economic divergence in Africa* (manuscript in preparation).

Until a `LICENSE` file is added, reuse permissions are not granted by this repository. Third-party datasets remain subject to their own licences and attribution requirements.

## Support

For questions about the implementation or underlying data preparation, contact the corresponding author listed in the manuscript.
