# ASX200_Screener
**Author:** A Tran 
**Project:** ASX200 Stock Screener for SIIF

## Project Overview
This repo contains a quantitative stock screening engine that identifies historical analogues for ASX 200 constituents. Current price-derived metrics are converted into Z-score space and searched against a historical database of 95,734 snapshots using K-Nearest Neighbours (KNN) in Euclidean distance space. For each input stock, the engine returns the K most similar historical observations, surfaces forward
return distributions across 1, 3, 6 and 12 month horizons, and generates entry/exit signals.

## Contents
- **`01_data_pipeline.ipynb`**: Universe definition, data extraction via yfinance, integrity audit, manual bridging of 17 gap stocks via
  DatAnalysis and foreign exchange suffixes, and final master dataset construction (189 stocks).
- **`02_similarity_engine.ipynb`**: Full screening pipeline: live metric snapshot engine (Momentum Z, Volatility Z, Idiosyncratic Volatility Z), historical Z-score database construction, KNN index fitting with liquidity pre-filter, analogue search, forward return matrix, probability distributions, entry/exit signals and fan chart visualisation.
- **`asx200.csv`**: The audited source-of-truth ticker list (198 active constituents as of 05/05/2026 - CTD and NSR suspended).
- **`manual_downloads`**: This folder contains the csvs of 4 name-change stocks: DNL, ELV, SGH, XYZ (downloaded converted from xls to csv)

## Methodology
- **Universe:** S&P/ASX 200 (May 2026 constituents) — 189 stocks successfully sourced
- **Data Sources:** yfinance (bulk + foreign-listed bridge), MorningStar DatAnalysis 
  (manual CSV export for 4 name-change stocks: DNL, ELV, SGH, XYZ)
- **Metric Normalisation:** All four signals converted to rolling Z-scores using expanding 
  windows (no lookahead bias) for cross-sector comparability
- **Similarity Search:** KNN with Euclidean distance across 4 dimensions — momentum_z, 
  volatility_z, idio_vol_z, dollar_vol_z — fitted on 95,734 historical snapshots
- **Historical Database:** Saved as CSV (parquet incompatible with Python 3.14)

## Setup & Usage
1. Install dependencies: `pip install yfinance pandas numpy scikit-learn matplotlib`
2. Run `01_data_pipeline.ipynb` to generate `ASX200_MASTER_DATASET.csv`
3. Run `02_similarity_engine.ipynb` to build the full pipeline and generate signals and fan charts for any ASX ticker

