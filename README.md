<p align="center">
  <img src="logos.png" alt="Water at the Heart of Climate Action — Ministry of Foreign Affairs of the Netherlands — World Meteorological Organization — HKV — Deltares" width="800"/>
</p>

<h1 align="center">WHCA — Urban Flash Flood Forecasting System (UFFFS)</h1>

<p align="center">
  <em>Training material for the Water at the Heart of Climate Action capacity-building workshops</em>
</p>

<p align="center">
  <a href="#about-the-programme">About</a> •
  <a href="#repository-overview">Overview</a> •
  <a href="#prerequisites">Prerequisites</a> •
  <a href="#installation">Installation</a> •
  <a href="#getting-started">Getting Started</a> •
  <a href="#notebooks">Notebooks</a> •
  <a href="#data-access">Data Access</a> •
  <a href="#license">License</a>
</p>

---

## About the Programme

**Water at the Heart of Climate Action (WHCA)** is a partnership between the [International Federation of Red Cross and Red Crescent Societies (IFRC)](https://www.ifrc.org/), the [World Meteorological Organization (WMO)](https://wmo.int/), the [United Nations Office for Disaster Risk Reduction (UNDRR)](https://www.undrr.org/), and the [Systematic Observations Financing Facility (SOFF)](https://alliancehydromet.org/soff/), funded by the **Ministry of Foreign Affairs of the Netherlands**. The programme supports climate-resilient water management and early warning systems in the Nile Basin region of East Africa.

As part of WHCA, [**HKV**](https://www.hkv.nl/en/) and [**Deltares**](https://www.deltares.nl/en) are implementing **Urban Flash Flood Forecasting Systems (UFFFS)** for five cities across five countries:

| Country | City |
|---|---|
| 🇪🇹 Ethiopia | Addis Abeba *(to be confirmed)*   |
| 🇷🇼 Rwanda | Kigali |
| 🇸🇸 South Sudan | Juba |
| 🇸🇩 Sudan | Khartoum |
| 🇺🇬 Uganda | Kampala |

Urban flash floods are among the most dangerous and challenging natural hazards in rapidly urbanising African cities. They occur within hours of extreme rainfall, develop very locally, and often strike low-income and informal settlements the hardest. The UFFFS combines real-time satellite rainfall observation, nowcasting, and hydrodynamic flood modelling into an end-to-end early warning chain — all built on open-source tools and openly available data, so that national meteorological and hydrological services can operate and maintain the system independently.

This repository contains the **training material** developed for the capacity-building workshops held during the programme. The notebooks are designed to be self-contained, hands-on tutorials that guide participants through every step of the UFFFS workflow.

---

## Repository Overview

The repository is organised into two independent notebook modules, each with its own Python environment:

```
WHCA_UFFFS/
├── README.md
├── LICENSE
├── logos.png
│
├── Notebooks/
│   ├── 1_Nowcasting/                          ← Satellite rainfall & nowcasting
│   │   ├── install.bat                        ← Run once to set up the environment
│   │   ├── start.bat                          ← Launch Jupyter Lab
│   │   ├── pixi.toml                          ← Environment definition
│   │   ├── enhanced_steps.py                  ← Enhanced STEPS nowcast engine
│   │   ├── __init__.py
│   │   ├── 1_Download_HSAF-H40B.ipynb         ← Download & preprocess satellite data
│   │   ├── 2_Nowcast_HSAF-H40B.ipynb          ← Create a STEPS rainfall nowcast
│   │   └── 3_Combination_HSAF-H40B_Nowcast.ipynb  ← Operational combined script
│   │
│   └── 2_Urban_Flash_Flood_Model/             ← Hydrodynamic flood modelling
│       ├── install.bat                        ← Run once to set up the environment
│       ├── start.bat                          ← Launch Jupyter Lab
│       ├── pixi.toml                          ← Environment definition
│       ├── 1_Run_DireDawa_SFINCS_model.ipynb  ← Inspect & run a pre-built SFINCS model
│       ├── 2_Build_Your_Own_Model.ipynb       ← Build a custom SFINCS model anywhere in East Africa
│       └── model_build_files/
│           ├── hydromt_east_africa_sfincs.yml ← HydroMT data catalog for East Africa
│           └── sfincs_build_my_own_model.yml  ← HydroMT build configuration
│
└── data/                                      ← Provided separately (see Data Access)
```

> **Why two separate environments?** The nowcasting module and the flood modelling module have different Python dependency requirements. Keeping them separate avoids version conflicts and makes each module independently installable.

---

## Prerequisites

### Install Pixi

All environments in this repository are managed with [**Pixi**](https://pixi.sh) — a fast, cross-platform package manager built on the conda ecosystem. Pixi reads a `pixi.toml` file and creates a reproducible, isolated Python environment with all required dependencies. You do **not** need to install Anaconda, Miniconda, or any other Python distribution beforehand.

#### What is Pixi?

Pixi is a modern package manager that replaces conda/mamba for managing scientific Python environments. It is fast, reproducible, and works on Windows, macOS, and Linux. Each project folder contains a `pixi.toml` file that defines exactly which packages and versions are needed — Pixi reads this file and creates a self-contained environment automatically.

#### How to Install Pixi

1. Go to the **Pixi installation page**: [https://pixi.sh/latest/#installation](https://pixi.sh/latest/#installation)

2. **On Windows** (recommended method), open **PowerShell** and run:
   ```powershell
   winget install prefix-dev.pixi
   ```
   Alternatively, you can use the installer script:
   ```powershell
   iwr -useb https://pixi.sh/install.ps1 | iex
   ```

3. **On macOS / Linux**, open a terminal and run:
   ```bash
   curl -fsSL https://pixi.sh/install.sh | bash
   ```

4. **Verify the installation** by opening a new terminal window and running:
   ```
   pixi --version
   ```
   You should see a version number (e.g., `pixi 0.45.0`). If you get a "command not found" error, close and reopen your terminal, or restart your computer.

> **Tip:** If you are behind a corporate proxy or firewall, see the [Pixi documentation](https://pixi.sh/latest/) for proxy configuration instructions.

---

## Installation

Each notebook folder contains two batch files that automate the entire setup. You only need to run the installation **once per module**.

### Step 1: Install the environment

Navigate to the notebook folder you want to use and **double-click `install.bat`** (or run it from a terminal). The script will:

1. Clean any previous environment
2. Download and install all Python dependencies via Pixi
3. Register a Jupyter kernel so the notebooks can find the environment

**For the Nowcasting module:**
```
cd Notebooks/1_Nowcasting
install.bat
```

**For the Urban Flash Flood Model module:**
```
cd Notebooks/2_Urban_Flash_Flood_Model
install.bat
```

> **Note:** The first installation may take several minutes as Pixi downloads all packages. Subsequent installs are much faster thanks to caching.

### Step 2: Launch Jupyter Lab

After installation, **double-click `start.bat`** (or run it from a terminal) to open Jupyter Lab in your browser:

```
start.bat
```

Jupyter Lab will open automatically. Navigate to the notebook you want to run and make sure the correct kernel is selected (see the kernel name in the top-right corner of the notebook).

### Quick Reference

| Action | Nowcasting | Urban Flood Model |
|---|---|---|
| Install (run once) | `1_Nowcasting/install.bat` | `2_Urban_Flash_Flood_Model/install.bat` |
| Start Jupyter Lab | `1_Nowcasting/start.bat` | `2_Urban_Flash_Flood_Model/start.bat` |
| Kernel name | `W@HCA UFFFS Nowcast (pixi)` | `W@HCA_UFFFS_Model (pixi)` |

---

## Getting Started

If you are new to this material, we recommend working through the notebooks in the following order:

### Part 1 — Satellite Rainfall & Nowcasting

These notebooks teach you how to access real-time satellite precipitation data, preprocess it, and create short-term rainfall forecasts (nowcasts) that can serve as input for the flood model.

1. **`1_Download_HSAF-H40B.ipynb`** — Start here. Learn to download and preprocess HSAF H40B satellite rainfall data from the EUMETSAT FTP server.
2. **`2_Nowcast_HSAF-H40B.ipynb`** — Use the preprocessed data to create a STEPS nowcast using pysteps.
3. **`3_Combination_HSAF-H40B_Nowcast.ipynb`** — An operational script that combines downloading, preprocessing, and nowcasting into a single automated workflow.

### Part 2 — Urban Flash Flood Modelling

These notebooks teach you how to set up and run a hydrodynamic flood model that translates rainfall into flood extent and depth maps.

4. **`1_Run_DireDawa_SFINCS_model.ipynb`** — Inspect and run a pre-built SFINCS flood model for Dire Dawa, Ethiopia. Understand model structure, inputs, and outputs.
5. **`2_Build_Your_Own_Model.ipynb`** — Build a custom SFINCS model for any location in East Africa using an interactive map and HydroMT.

---

## Notebooks

### Module 1: Satellite Rainfall & Nowcasting

#### Notebook 1 — Download, Preprocess, and Analyse HSAF H40B

This notebook is the entry point for working with satellite precipitation data. It guides you through:

- Connecting to the EUMETSAT HSAF FTP server and downloading H40B data files
- Understanding the MTG FCI instrument and its geostationary projection
- Converting angular coordinates (radians) to geographic coordinates using the satellite projection parameters
- Regridding the native satellite grid to a regular latitude/longitude grid
- Extracting precipitation for a specific region of interest
- Visualising rainfall accumulations and time series

**Key concept:** H40B is derived from the Meteosat Third Generation (MTG) Flexible Combined Imager (FCI) and provides precipitation estimates at **10-minute intervals** with a spatial resolution of approximately 2 km over Africa.

#### Notebook 2 — Create a STEPS Nowcast

Building on the preprocessed data from Notebook 1, this tutorial shows you how to:

- Load a time series of preprocessed rainfall fields into a 3D dataset (x, y, time)
- Configure the STEPS nowcast model parameters (lead time, ensemble members, domain)
- Run the nowcast using the `EnhancedStepsNowcast` engine (provided in `enhanced_steps.py`)
- Visualise and interpret the nowcast output (ensemble mean, probability maps)

**Key concept:** STEPS (Short-Term Ensemble Prediction System) is a widely used nowcasting method that extrapolates observed rainfall patterns forward in time using optical flow, while adding stochastic perturbations at different spatial scales to account for forecast uncertainty.

#### Notebook 3 — Operational Combination Script

This notebook provides a streamlined, operational version of the full observation-to-nowcast pipeline. It is designed for production use rather than learning:

- Configure settings once at the top (date selection, output formats)
- Supports both **real-time** mode (automatically selects the most recent data) and **historical** mode (user-specified date)
- Outputs: GIF animations, Excel time series, and static graphs — all saved automatically

### Module 2: Urban Flash Flood Modelling

#### Notebook 4 — Run the Dire Dawa SFINCS Model

A comprehensive, step-by-step guide to understanding and running a pre-built hydrodynamic flood model:

- Understanding the SFINCS model structure and input files (`sfincs.inp`, elevation grids, forcing files)
- Inspecting model configuration: grid definition, resolution, simulation period
- Running the SFINCS simulation
- Analysing and visualising flood outputs: water depth maps, flood extent, time series

**Key concept:** SFINCS (Super-Fast INundation of CoastalS) is an open-source, computationally efficient hydrodynamic model capable of simulating compound flooding (pluvial, fluvial, and coastal). Its speed makes it particularly well-suited for real-time forecasting applications.

#### Notebook 5 — Build Your Own Model

An interactive notebook for creating a custom SFINCS model anywhere in East Africa:

- Use an interactive map to select your model region
- Define a bounding polygon and export it as GeoJSON
- Configure model parameters: grid resolution, simulation period, boundary conditions
- Automated model building using HydroMT-SFINCS with openly available datasets:
  - **Elevation:** Copernicus DEM GLO-30 (30m resolution)
  - **Land use:** ESA WorldCover 2021
  - **Soil:** SoilGrids 2.0 and GCN250 curve numbers
  - **Hydrography:** MERIT Hydro
- Design storm configuration with realistic parameterisation for the East African context

---

## Data Access

The notebooks require input data (satellite rainfall files, pre-built model data, elevation datasets) that is **not included** in this repository due to file size.

> **📧 To obtain the data, please contact [j.aerts@hkv.nl](mailto:j.aerts@hkv.nl)**

Additionally, for the satellite rainfall notebooks, you will need to register for an HSAF account to access the FTP server:

- **HSAF registration:** [https://hsaf.meteoam.it/User/Register](https://hsaf.meteoam.it/User/Register)

---

## Key Technologies

| Component | Technology | Description |
|---|---|---|
| Satellite rainfall | [HSAF H40B](https://hsaf.meteoam.it/) | Precipitation estimates from the MTG FCI instrument |
| Nowcasting | [pysteps](https://pysteps.readthedocs.io/) | Short-term ensemble prediction of precipitation |
| Flood modelling | [SFINCS](https://sfincs.readthedocs.io/) | Fast hydrodynamic flood simulation |
| Model building | [HydroMT-SFINCS](https://deltares.github.io/hydromt_sfincs/) | Automated SFINCS model setup from open datasets |
| Environment management | [Pixi](https://pixi.sh) | Reproducible conda-based environments |
| Notebooks | [Jupyter Lab](https://jupyter.org/) | Interactive computing platform |

---

## Troubleshooting

**"pixi not found" when running install.bat**
Make sure Pixi is installed (see [Prerequisites](#prerequisites)) and that you opened a **new** terminal window after installation.

**Installation fails with dependency conflicts**
Try running `pixi clean` in the notebook folder, then `install.bat` again. If the problem persists, ensure you have a stable internet connection and that no VPN or firewall is blocking access to `conda-forge`.

**Wrong kernel in Jupyter**
After opening a notebook, check the kernel name in the top-right corner. Use **Kernel → Change Kernel** and select the correct one (see the [Quick Reference](#quick-reference) table).

**GDAL/rasterio DLL errors on Windows**
This typically indicates a version mismatch. Running `install.bat` again (which calls `pixi clean` first) usually resolves this.

**FTP connection to HSAF fails**
Verify your HSAF credentials at [https://hsaf.meteoam.it/](https://hsaf.meteoam.it/). Some institutional networks block FTP connections — try using a personal network or VPN.

---

## Contributing

This material is developed as part of the WHCA programme. If you find issues or have suggestions for improvement, please open an issue on this repository or contact the development team.

---

## Contact

For questions about the workshop material, data access, or the WHCA UFFFS programme:

📧 **Jerom Aerts** — [j.aerts@hkv.nl](mailto:j.aerts@hkv.nl)

---

## License

This repository is released under the [CC0 1.0 Universal](LICENSE) public domain dedication. You can copy, modify, and distribute the material.

---

<p align="center">
  <sub>Developed by <a href="https://www.hkv.nl/en/">HKV</a> and <a href="https://www.deltares.nl/en">Deltares</a> for the <a href="https://wmo.int/">World Meteorological Organization</a> as part of the Water at the Heart of Climate Action programme, funded by the Ministry of Foreign Affairs of the Netherlands.</sub>
</p>
