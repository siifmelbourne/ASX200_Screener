# ASX200_Screener
**Author:** A Tran 
**Project:** ASX200 Stock Screener for SIIF

## Project Overview
This repository contains the foundation for a quantitative stock screening engine that identifies historical analogues for ASX 200 constituents. By converting current price-derived metrics into Z-score space, we can search for historical periods with similar risk/return profiles using Euclidean distance.

## Contents
- **`01_data_pipeline.ipynb`**: Handles universe definition, data extraction from `yfinance`, and integrity auditing with `MorningStar DatAnalysis` (identifying 17 gaps like XYZ and NEM for manual bridging). 
- **`02_similarity_engine.ipynb`**: Implementation of the live metric engine. Calculates Momentum Z, Volatility Z, and Idiosyncratic Volatility for current portfolio holdings.
- **`asx200.csv`**: The audited source-of-truth ticker list (198 active constituents as of 05/05/2026 - CTD and NSR suspended).

## Methodology
- **Universe:** S&P/ASX 200 (May 2026 constituents).
- **Data Sources:** `yfinance` (Live/Daily) and `MorningStar DatAnalysis` (Historical Bridge).
- **Metric Normalisation:** All signals are converted to rolling Z-scores to ensure cross-sector comparability and mitigate scale bias in the similarity search.

## Setup & Usage
1. Ensure all libraries are installed.
2. Run `01_data_pipeline.ipynb` to generate the local price history database.
3. Run `02_similarity_engine.ipynb` to view live metric snapshots for specific tickers.
