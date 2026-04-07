# Advanced Research Data Management to Enhance Reuse and Societal Impact of Flux Data

## Overview
This repository demonstrates a **practical research data management (RDM) workflow** for eddy covariance (EC) data using:

- DBRepo → versioned, semantically annotated data storage  
- ERA5 → external reanalysis dataset for comparison  

Focus:
1. **Versioning** (temporal data evolution)  
2. **Interoperability** (semantic alignment EC ↔ ERA5)  

---

## Repository Contents
- `ec_tidbrepo_versioning.ipynb` — DBRepo temporal versioning demonstration  
- `ec_tidbrepo_interoperability.ipynb` — semantic mapping and EC–ERA5 comparison  
- `fec44b0aec5937106a8315efec5fcfbe.grib` — ERA5 data  

---

## Workflow

### 1. Versioning (DBRepo)
- Data is never overwritten  
- Updates create new row versions  
- Enables querying dataset at any time  

Key idea:
> Dataset = evolving system, not static file  

---

### 2. ERA5 Processing
- Load GRIB using `xarray + cfgrib`  
- Variables loaded separately (`t2m`, `slhf`, `sshf`)  
- Flatten `(time, step)` → `valid_time`  

---

### 3. Semantic Mapping

| Semantic Class      | EC Variable       | ERA5 Variable |
|--------------------|-----------------|--------------|
| air_temperature     | air_temperature  | t2m          |
| latent_heat_flux    | le               | slhf         |
| sensible_heat_flux  | h                | sshf         |

---

### 4. Unit Conversion

ERA5 fluxes are accumulated energy (J m⁻²):

    flux (W m⁻²) = flux / 3600

---

### 5. Time Alignment
- ERA5: UTC  
- EC: MYT (UTC+8)  

---

## Key Concepts

### Versioning
- Row-level history (`ts_add`, `ts_delete`)  
- Full reproducibility  
- No data loss  

### Semantics
- Concept URI + unit URI per variable  
- Enables machine-readable interoperability  

### Interoperability
- Mapping based on meaning, not variable names  

---

## Why This Matters
- Reproducible science  
- FAIR data principles  
- Robust EC–model comparison  

---

## Requirements

    pip install pandas xarray cfgrib cdsapi dbrepo

---

## Author
Yusri Yusup  
School of Industrial Technology  
Universiti Sains Malaysia
