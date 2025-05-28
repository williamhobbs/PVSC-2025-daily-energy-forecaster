# PVSC-2025-daily-energy-forecaster

Will Hobbs and Drumil Joshi, 2025

This repository contains code and other supporting details related to the IEEE PVSC 2025 talk and manuscript, *Using Open-Source Forecasts for Solar Plant Maintenance Outage Scheduling can Reduce Lost Energy*, by William B. Hobbs and Drumil Joshi. 

This project uses several packages, but most notably leverages pvlib [1], an open-source solar PV modeling package, and Herbie [2], a Python package for accessing numerical weather prediction (NWP) model outputs from different sources.

<img src="images/pvlib_powered_logo_horiz.png" width="200"/>

## Using this repository

Start with the steps in the [Setup](#setup) section below. Then, review the Jupyter notebook files in order/

- [01_Get_ERCOT_EIA_Data.ipynb](01_Get_ERCOT_EIA_Data.ipynb)
- [02_Make_Forecasts.ipynb](02_Make_Forecasts.ipynb)
- [03_Analysis.ipynb](03_Analysis.ipynb)
- [04_Make_Ensemble_Forecasts.ipynb](04_Make_Ensemble_Forecasts.ipynb)
- [05_Ensemble_Analysis.ipynb](05_Ensemble_Analysis.ipynb)



## Setup

### Environment and common packages
I used [Miniforge](https://github.com/conda-forge/miniforge?tab=readme-ov-file#install) to create an environment and then a mix of `conda` and `pip` to install packages, like:

```
conda create -n pvsc_forecaster_2025 python=3.12 -y
conda activate pvsc_forecaster_2025
conda install -c conda-forge herbie-data
pip install gridstatusio openpyxl python-Levenshtein thefuzz pvlib
pip install pandas matplotlib ipykernel jupyter
```

*Note: Before April 2025 it was difficult to install Herbie on Windows without `conda`. Apparently that changed when `eccodes` became available via `pip`. See [3], but I haven't tried this yet.*

### Custom packages
Then get two additional Python files:
- `forecast_solar.py` from https://github.com/williamhobbs/energy-forecasting-tools
- `pv_model.py` from https://github.com/williamhobbs/pv-system-model

and place them in the directory you are using. 

### GridStatus.io API Key
This project uses power data from real power plants in ERCOT. Data are available directly from ERCOT, but here we use the API from [gridstatus.io](https://www.gridstatus.io/) to simplify things. As written, the code here requires users to get their own API key from [gridstatus.io](https://www.gridstatus.io/) and place it in a file named `gridstatus_api_key.txt` in the working directory. 

Alternatively, data are avialable directly from ERCOT [4] after free registration, but downloading and formatting the data are outside of the current scope of this repository. 

-----

[1] Anderson, K., Hansen, C., Holmgren, W., Jensen, A., Mikofski, M., and Driesse, A. “pvlib python: 2023 project update.” Journal of Open Source Software, 8(92), 5994, (2023). [DOI: 10.21105/joss.05994](http://dx.doi.org/10.21105/joss.05994). (https://github.com/pvlib/pvlib-python)

[2] Blaylock, B. K. (2025). Herbie: Retrieve Numerical Weather Prediction Model Data (Version 2025.3.1) [Computer software]. https://doi.org/10.5281/zenodo.4567540 (https://github.com/blaylockbk/Herbie/)

[3] https://github.com/blaylockbk/Herbie/discussions/428

[4] https://data.ercot.com/data-product-archive/NP3-965-ER