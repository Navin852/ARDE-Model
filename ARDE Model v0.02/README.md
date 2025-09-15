# ARDE Model – Automated Rainfall Data Evaluation Model
The ARDE Model (Automated Rainfall Data Extraction Model) is a Python-based pipeline that automates the downloading, processing, and comparison of rainfall data from multiple sources, including:

- **NWIC** (Standard Rain Gauge)

- **IMD** (Gridded Rainfall Data)

- **ERA5** (Reanalysis Data from ECMWF)

- **CHIRPS** (Climate Hazards Group InfraRed Precipitation)

- **GPM IMERG** (Satellite-based Rainfall Estimates)

By integrating these datasets, ARDE allows researchers to:

- Cross-validate ground and satellite rainfall data

- Assess satellite product accuracy

- Analyze long-term rainfall trends for hydrology, disaster management, and climate studies

# 📌 Getting Started
# 1. Clone the Repository

```bash
git clone https://github.com/your-username/ARDE-Model.git
cd ARDE-Model
```
# 2. Prerequisites
Before running the ARDE Model, ensure you have:

- **Station Data (NWIC):** Original NWIC CSV file (manual SRG)

- **CDS API Key** (for ERA5) → Create an account at CDS and set up your .cdsapirc file

- **Google Earth Engine Account** → Sign up here

- **GEE Project ID** (for CHIRPS extraction)

- **Earthdata Account** → Register here for GPM IMERG downloads

```bash
pip install -r requirements.txt
```
# 📂 Data Placement
- `config.yaml` → Place in the root folder of the repository.
This file stores station metadata, coordinates, date ranges data directories, and Authendication credentials.
- **Raw NWIC CSV** → also place in the repo root, named e.g. `Rainfall_Murappanadu.csv`.
Example `config.yaml`:
```yaml
station_name: "Murappanadu"
lat: 8.7144
lon: 77.835
start_date: "2022-01-01"
end_date: "2024-12-31"
data_dir: ./data         # ARDE will create subfolders like ./data/NWIC
output_dir: ./results    # used by other modules
cds_url: "https://cds.climate.copernicus.eu/api"
cds_key: "enter-the-key"
gee_project_id: "enter-your-project-ID"

```

# ▶️ Run ARDE Model
- Put `config.yaml` and your raw **NWIC CSV** in the repo root.

- Open `ARDE.ipynb` (or run the provided script).

- Execute the Following Cell/Script.


# 🔐 Credentials (for ERA5/IMERG/CHIRPS modules)
- **ERA5 (CDS):** save your key in `~/.cdsapirc`

- **IMERG (Earthdata):** `earthaccess.login()` once per session

- **CHIRPS (GEE):** `ee.Authenticate()` and set your Project ID

# 🧪 Reproducibility & Structure
- All paths are resolved relative to `config.yaml` so collaborators can run the model with their own folders by editing only that file.

- Submodules (ERA5/CHIRPS/IMERG) write into `<data_dir>/<source>/` consistently.


# ❓Troubleshooting
- **File not found:** confirm config.yaml and raw NWIC CSV are in the repo root.

- **Windows paths:** avoid spaces in folder names if possible; keep them quoted in YAML.

- **Wrong station period:** check start_date/end_date in config.yaml.

# ✅ Best Use Conditions & Future Enhancements
- **Data Quality Dependency**
Model accuracy is sensitive to rain gauge data completeness; excessive NA values reduce validation reliability and bias performance metrics.
- **Single-Station Operation**
Currently restricted to one station per run; batch processing for multiple stations is not yet supported.
- **Storage and Memory Requirements**
Large reanalysis/satellite datasets (GBs per year) may exceed low storage or RAM capacity during processing.

ARDE works best when NWIC station data is complete with minimal missing values, the system has sufficient computing resources, and external API services are available. With future updates, support for multi-station runs, faster performance, and advanced error metrics could overcome current limitations
