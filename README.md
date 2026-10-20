# Uneven multimodal transport expansion reshapes regional economic divergence in Africa

This repository contains the Python notebooks used for the analyses in *Uneven multimodal transport expansion reshapes regional economic divergence in Africa*. The study evaluates associations between the expansion of roads, paved highways, railways, railway stations, ports, and aviation infrastructure and economic growth, sectoral development, individual welfare, and wealth inequality across African countries from 2015 to 2024.

## Repository contents


| Notebook                                            | Purpose                                                                                                                                      |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `01_process_osm_infrastructure.ipynb`               | Extract transport infrastructure layers from OpenStreetMap PBF snapshots.                                                                    |
| `02_clip_infrastructure_to_africa_arcpy.ipynb`      | Clip annual infrastructure layers to the African study area (ArcPy).                                                                         |
| `03_project_infrastructure_layers_arcpy.ipynb`      | Project infrastructure layers and calculate length/area attributes (ArcPy).                                                                  |
| `04_project_administrative_boundaries_arcpy.ipynb`  | Project administrative boundaries and calculate areas (ArcPy).                                                                               |
| `05_process_wealth_inequality_data.ipynb`           | Harmonize World Inequality Database records and construct wealth-distribution indicators.                                                    |
| `06_psm_did_railway_impact.ipynb`                   | Estimate the Addis Ababa-Djibouti railway effect using PSM-DID and event-study checks.                                                       |
| `07_system_gmm_robustness_checks.ipynb`             | Run dynamic-panel system-GMM robustness analyses.                                                                                            |
| `08_multimodal_transport_economic_divergence.ipynb` | Map GDP and six transport infrastructure types, export infrastructure-growth data, and plot growth trends and associations.                  |
| `09_mode_specific_sectoral_effects.ipynb`           | Map mode-specific sectoral correlations and compare country, regional, and continental growth-rate associations and sector specificity.      |
| `10_multiscale_transport_economic_effects.ipynb`    | Analyze lagged growth-rate correlations, regional-interaction and nested multiscale models, model diagnostics, and cumulative effects.       |
| `11_transport_welfare_and_inequality.ipynb`         | Map scale-adjusted infrastructure residuals and assess transport-growth associations with welfare and population-weighted wealth inequality. |

## Software requirements

The analyses were developed with Python 3.11.3. Create an isolated environment and install the public Python dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

The preprocessing notebooks `02`--`04` require ArcPy and therefore an active ArcGIS Pro installation. ArcPy is proprietary and is intentionally not included in `requirements.txt`. Run notebooks `01` and `05`--`11` in the Python environment above; run notebooks `02`--`04` with the Python environment supplied by ArcGIS Pro.

## Data sources

The repository contains code only. Download data from the original providers and comply with their current terms of use before running the notebooks.


| Dataset                       | Use in this study                                                                                           | Source                                                                            |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| OpenStreetMap Africa extracts | Roads, paved highways, railways, railway stations, ports, and aviation infrastructure                       | [Geofabrik](https://download.geofabrik.de/africa.html)                            |
| Administrative boundaries     | Country and subregion spatial layers                                                                        | [Natural Earth](https://www.naturalearthdata.com/)                                |
| African macroeconomic data    | GDP, GDP per capita, population, exchange rates, price indices, and household final consumption expenditure | [African Development Bank data portal](https://dataportal.opendataforafrica.org/) |
| Sectoral value added          | Agriculture, industry, and services                                                                         | [World Bank Open Data](https://data.worldbank.org/)                               |
| Wealth-distribution data      | Top 1%, top 10% and bottom 50% wealth shares                                                                | [World Inequality Database](https://wid.world/world/)                             |

## Configuration and execution

The notebooks use English-only local paths. The expected data layout is:

```text
E:\Africa_Infrastructure_Data\
├── infrastructure\
│   └── clip_project\
│       └── <year>\
├── boundaries\
├── boundaries_project\
├── boundaries_project_49\
├── wid\
├── afdb\
├── world_bank\
├── transport_statistics_2015_2025.xlsx
└── wealth_inequality_2015_2024.xlsx
```

On another computer, create the same directory layout (or update the path variables near the top of each notebook) and place the downloaded data in the corresponding locations. Run notebooks from this repository directory so that relative output paths resolve consistently. Notebook `08` writes intermediate growth tables, normalization parameters, and spatial layers to `outputs/multimodal_transport_economic_divergence/`. Figures are displayed inline; only explicit export calls write files to disk.

### CARTO basemap configuration

Notebooks `08`, `09`, and `11` use the CARTO Positron No Labels basemap through `contextily` and `xyzservices.TileProvider`. They read a basemap key from the `CARTO_BASEMAP_KEY` environment variable, or prompt for it with `getpass` when the variable is absent. Obtain a key from the [CARTO Basemaps key request page](https://carto.com/basemaps/apikey/).

For a Windows PowerShell session, set the variable before starting Jupyter:

```powershell
$env:CARTO_BASEMAP_KEY = 'YOUR_CARTO_BASEMAP_KEY'
jupyter lab
```

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

## Code availability and citation

Please cite the associated manuscript when using or adapting this code:

> *Uneven multimodal transport expansion reshapes regional economic divergence in Africa* (manuscript in preparation).

Until a `LICENSE` file is added, reuse permissions are not granted by this repository. Third-party datasets remain subject to their own licences and attribution requirements.

## Support

For questions about the implementation or underlying data preparation, contact the corresponding author listed in the manuscript.
