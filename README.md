# Gironde Wildfire Risk Watch

An experimental machine learning project to study and model short-term wildfire risk in **Gironde, France**, using meteorological and Earth-observation data.

The project starts as a scientific ML study and is intended to evolve progressively into a reproducible daily wildfire-risk monitoring system.

> **Status:** early development — data reconnaissance and project setup.

## Project goals

This project is designed to:

- study whether recent weather conditions can help predict short-term wildfire occurrence in Gironde;
- learn and apply spatio-temporal data processing and Earth Observation;
- compare classical machine-learning and deep-learning approaches;
- study calibration, generalisation and environmental distribution shift;
- explore long-term changes in weather conditions associated with wildfire risk;
- build the project using sound software-engineering and reproducibility practices;
- progressively turn the validated model into an observable, containerised ML system.

The project is also intended as a learning and portfolio project in environmental AI, scientific machine learning and ML engineering.

## Initial research question

> **Can recent meteorological conditions predict short-term wildfire occurrence in Gironde?**

The first version of the project will use approximately **14 days of recent weather** to estimate the probability of a wildfire occurring within the following **3 days**.

The initial modelling ladder will be:

1. constant / prevalence baseline;
2. seasonal baseline;
3. Logistic Regression;
4. XGBoost;
5. temporal deep learning with Keras / TensorFlow.

More advanced Earth-observation, robustness, climate and ML-systems work will only be added after the baseline is complete.

## Study area

The primary study area is **Gironde, France**.

If Gironde alone does not provide enough positive wildfire observations for reliable model training, the training domain may be expanded to nearby areas such as the Landes or Nouvelle-Aquitaine while keeping Gironde as a primary evaluation and interpretation region.

## Data

The first stages of the project are expected to use:

- **ERA5-Land** for historical meteorological data;
- **BDIFF** for historical wildfire records in France;
- French administrative boundaries for spatial alignment.

Later extensions may use:

- **Sentinel-2** for vegetation and moisture indicators such as NDVI, NDMI or NBR;
- **NASA FIRMS / VIIRS** for active-fire observations and case studies.

Raw external datasets are not intended to be committed to Git. Data acquisition and processing steps should instead be reproducible from documented sources and configuration.

## Planned project stages

### 1. Data reconnaissance

- inspect Gironde administrative boundaries;
- inspect BDIFF wildfire records;
- download and inspect a small ERA5-Land sample;
- align wildfire and weather data spatially;
- decide whether the baseline prediction unit should be an ERA5 grid cell or a commune.

### 2. Historical dataset

- build daily weather variables;
- create 14-day weather histories;
- create 3-day future wildfire labels;
- define chronological train / validation / test splits;
- implement leakage and data-quality tests.

### 3. Classical machine learning

- prevalence and seasonal baselines;
- Logistic Regression;
- XGBoost;
- rare-event evaluation;
- calibration and feature ablations.

### 4. Temporal deep learning

- build weather-sequence datasets;
- train a small LSTM or TCN with Keras / TensorFlow;
- compare learned temporal representations with engineered features.

### 5. Earth Observation

- add Sentinel-2 vegetation / moisture information;
- compare weather-only and weather + EO models;
- optionally perform burned-area segmentation with PyTorch.

### 6. Robustness and climate analysis

- evaluate temporal and geographic generalisation;
- study calibration under environmental distribution shift;
- analyse long-term changes in fire-conducive weather conditions.

### 7. ML engineering and systems

- package the scientific code;
- add automated tests and CI;
- track experiments and model versions with MLflow;
- containerise the workloads;
- expose persisted predictions through FastAPI;
- build a simple dashboard;
- automate daily inference;
- deploy with Kubernetes;
- monitor data, pipeline and service health with Prometheus / Grafana;
- benchmark relevant CPU / GPU workloads.

### 8. Gironde Wildfire Risk Watch

The final system should operate as a **daily batch pipeline**:

```text
recent weather
      ↓
data validation
      ↓
feature generation
      ↓
registered model
      ↓
batch inference
      ↓
stored risk predictions
      ↓
API + dashboard
```

A historical replay mode will be implemented before any live or near-live deployment.

## Technical stack

The stack will be introduced progressively rather than all at once.

**Scientific and geospatial data**

- Python
- NumPy
- pandas
- xarray
- NetCDF / Zarr
- GeoPandas
- Shapely
- Rasterio / rioxarray

**Machine learning**

- scikit-learn
- XGBoost
- TensorFlow / Keras
- PyTorch

**Engineering and ML systems**

- pytest
- Ruff
- pre-commit
- MLflow
- FastAPI
- Streamlit
- Docker
- GitHub Actions
- Kubernetes
- Prometheus
- Grafana

Additional tools will only be added when they solve a concrete project need.

## Repository structure

The repository will evolve over time. The intended structure is approximately:

```text
gironde-wildfire-risk/
├── README.md
├── PROJECT_SPEC.md
├── DATA.md
├── EXPERIMENTS.md
├── MODEL_CARD.md
├── SYSTEM.md
├── pyproject.toml
├── configs/
├── data/
│   ├── raw/
│   ├── external/
│   ├── interim/
│   └── processed/
├── notebooks/
├── src/
│   └── wildfire_watch/
├── scripts/
├── tests/
├── apps/
├── benchmarks/
├── deployment/
└── reports/
```

Notebooks are intended primarily for exploration and analysis. Reusable project logic should live under `src/`.

## Getting started

The project is currently in its setup and data-reconnaissance phase.

### 1. Clone the repository

```bash
git clone <repository-url>
cd gironde-wildfire-risk
```

### 2. Create the Python environment

The exact environment setup will be documented once the initial dependencies are frozen.

The project will use a reproducible `pyproject.toml`-based environment, preferably managed with `uv`.

### 3. Start with data reconnaissance

The first milestone is intentionally small:

1. load the Gironde boundary;
2. inspect BDIFF wildfire records;
3. download one month of ERA5-Land data;
4. visualise the wildfire records and weather grid together;
5. inspect wildfire counts by year and month;
6. decide the safest spatial representation for the modelling dataset.

## Development principles

The project follows a few simple rules:

- **science first, system second, live Watch last;**
- prefer simple baselines before complex models;
- use chronological evaluation for forecasting;
- treat data leakage as a critical failure;
- preserve realistic class imbalance in validation and test data;
- report negative results;
- do not interpret feature importance as causality;
- do not overstate the spatial precision of wildfire records;
- do not make causal climate-change claims from correlation alone;
- keep raw data immutable;
- keep reusable logic out of notebooks;
- version code, configuration, datasets and model artifacts wherever practical;
- prefer no prediction over a silently invalid or stale Watch prediction.

## Safety and limitations

This project is **experimental research software**.

It is not an official wildfire-warning system and must not be used for emergency decisions, evacuation guidance or public-safety operations.

Any future dashboard or risk category must clearly distinguish experimental model output from official wildfire-danger information.

## Documentation

The project will progressively maintain:

- `PROJECT_SPEC.md` — full scientific and engineering specification;
- `DATA.md` — data sources, schemas, provenance and limitations;
- `EXPERIMENTS.md` — experiment history and results;
- `MODEL_CARD.md` — model scope, performance and limitations;
- `SYSTEM.md` — operational architecture, deployment and monitoring.

## License

To be selected. 

External datasets remain subject to their respective licences and terms of use.
