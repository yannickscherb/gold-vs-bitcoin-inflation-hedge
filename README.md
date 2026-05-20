# Gold vs. Bitcoin: Inflation Hedging Across Macroeconomic Regimes (2016–2025)

Replication code for the Bachelor thesis of the same title, examining whether gold and Bitcoin act as inflation hedges in four countries (United States, Switzerland, Japan, Argentina) over the period from January 2016 to December 2025.

**Author:** Yannick Scherb
**Supervisor:** Jan-Alexander Posth
**Institution:** ZHAW School of Management and Law
**Year:** 2026

## Overview

The empirical analysis estimates country-specific inflation betas for gold and Bitcoin by regressing monthly real asset returns on year-over-year CPI inflation and the prevailing central bank policy rate. Inference is based on Newey–West (HAC) standard errors with four lags. The analysis is conducted for the full 2016–2025 sample and separately for three macroeconomic sub-periods: pre-COVID (2016–2019), the COVID and inflation surge (2020–2022), and the monetary tightening cycle (2023–2025). Robustness is examined using nominal returns and month-over-month inflation.

## Repository Structure

```
.
├── Bachelor_thesis.ipynb       Main analysis notebook
├── README.md                   This file
├── requirements.txt            Python dependencies
├── LICENSE                     MIT licence
├── .gitignore                  Files excluded from version control
├── figures/                    Generated charts (PNG)
└── tables/                     Generated regression and summary tables (CSV)
```

The folders `data/raw/` and `data/processed/` are required for the notebook to run but are not included in this repository (see below).

## Data

Raw data are not redistributed here in order to respect the licence terms of commercial providers. To reproduce the analysis, the following files must be obtained and placed in `data/raw/` using exactly the filenames listed:

| File | Source |
|------|--------|
| `BTC_USD.csv` | Investing.com – Bitcoin historical data |
| `XAU_USD.csv` | Investing.com – Gold historical data |
| `USD_CHF.csv` | Investing.com – USD/CHF historical data |
| `USD_JPY.csv` | Investing.com – USD/JPY historical data |
| `USD_ARS.csv` | Investing.com – USD/ARS historical data |
| `CPI_USA.csv` | FRED – CPIAUCSL |
| `CPI_Switzerland.csv` | Swiss National Bank data portal – LIK (LD2010100) |
| `CPI_Japan.csv` | Statistics Bureau of Japan – CPI Indices of Items |
| `CPI_Argentina_Jan15-Dec16.xlsx` | BCRA – Monthly inflation (% change) |
| `CPI_Argentina_Dec16_-_now.xls` | INDEC – IPC Cobertura Nacional |
| `Policy_Rate_USA.csv` | FRED – FEDFUNDS |
| `Policy_Rate_Switzerland.csv` | Swiss National Bank data portal – snboffzisa |
| `Policy_Rate_Japan.csv` | Swiss National Bank data portal – Policy interest rate (Japan) |
| `Policy_Rate_Argentina.xlsx` | BCRA – Monetary policy rate |

All series are at monthly frequency. The CPI series must start in January 2015, because an additional year of data before the analysis window is required to compute year-over-year inflation. Asset prices, exchange rates and policy rates are needed from January 2016 onward. The analysis window itself runs from January 2016 to December 2025; the notebook aligns all dates to end-of-month timestamps and derives all subsequent variables (returns, real returns, inflation rates, real interest rate proxy).

Detailed URLs for each source are listed in the data sources section of the accompanying thesis.

## Reproducing the Analysis

1. Clone the repository and create the data directories:
```bash
   git clone https://github.com/<your-username>/gold-vs-bitcoin-inflation-hedge.git
   cd gold-vs-bitcoin-inflation-hedge
   mkdir -p data/raw data/processed
```
2. Download the raw data files listed above and place them in `data/raw/` using the exact filenames given.
3. Install dependencies:
```bash
   pip install -r requirements.txt
```
4. Open `Bachelor_thesis.ipynb` in Jupyter and run all cells sequentially. The notebook will load and clean the raw data, construct the four country-level panel datasets in `data/processed/`, produce all figures in `figures/` and tables in `tables/`, and print the full regression output for the main specification, the robustness checks and the sub-period analysis.

The analysis was developed and run with Python 3.13.

## Methodology in Brief

For each country and each asset, the main specification is

R<sub>real,t</sub> = α + β<sub>1</sub> · π<sub>YoY,t</sub> + β<sub>2</sub> · i<sub>t</sub> + ε<sub>t</sub>,

where R<sub>real,t</sub> is the monthly real return on the asset in local currency, π<sub>YoY,t</sub> is year-over-year CPI inflation, and i<sub>t</sub> is the central bank policy rate (in percent). The coefficient β<sub>1</sub> is the inflation beta. Standard errors are Newey–West HAC with four lags. For the United States, no currency conversion is applied; for Switzerland, Japan and Argentina, USD asset prices are converted into local currency before returns are computed.

## Declaration of AI Tools

Generative AI tools were used in the preparation of the accompanying thesis and in the setup of this repository. Claude (Anthropic, Opus 4.6) was used for the revision and refinement of draft text passages, for the generation and debugging of the Python code for data processing, regression estimation, and the creation of figures and tables, and for setting up this repository (drafting the README, the dependency list, the licence and the gitignore configuration). ChatGPT (OpenAI, GPT-4o) was used for the summarisation of academic literature and for text revision. The full declaration of AI use for the thesis is included in the thesis itself.

## Licence

This project is licensed under the MIT Licence – see the `LICENSE` file for details.