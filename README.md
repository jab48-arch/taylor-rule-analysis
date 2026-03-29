# Taylor Rule vs. Federal Funds Rate

An empirical analysis of Federal Reserve monetary policy discretion, comparing 
the actual federal funds rate against Taylor Rule prescriptions from 1991 to 
present using FRED data, Python, and OLS regression.

## Research Question

To what extent does the Federal Reserve deviate from Taylor Rule prescriptions 
during periods of economic shock, and what does this reveal about Fed discretion?

## Methodology

**Data Sources (FRED)**
- `FEDFUNDS` — Federal funds effective rate (monthly, resampled to quarterly)
- `CPIAUCSL` — CPI, converted to year-over-year inflation
- `GDPC1` / `GDPPOT` — Real and potential GDP, used to calculate the output gap

**Taylor Rule Formula**

r = 2 + π + 0.5(π − 2) + 0.5(output gap)

Where π is year-over-year CPI inflation and the output gap is 
((Real GDP − Potential GDP) / Potential GDP) × 100.

**OLS Regression**

The actual fed funds rate is regressed on the Taylor Rule prescription to 
quantify how closely the Fed followed the rule over the sample period.

## Key Findings

- The Fed remained consistently below the Taylor Rule prescription for most of 
  the sample period, suggesting a systematic dovish bias.
- During periods of significant economic shock (2008–2009, 2020), the prescribed 
  rate fell sharply negative while the Fed was constrained by the zero lower 
  bound — the most pronounced divergences in the sample.
- OLS results (R² = 0.19, coef = 0.34) indicate the Taylor Rule explains only 
  19% of Fed behavior, and the Fed responds less than half as aggressively as 
  the rule prescribes. High Durbin-Watson autocorrelation statistic (0.08) reflects the 
  inherent stickiness of interest rate policy.

## Setup

**Dependencies**
```
pip install pandas matplotlib statsmodels fredapi python-dotenv
```

**API Key**

Create a `.env` file in the project root:
```
FRED_API_KEY=your_key_here
```

FRED API keys are free at [fred.stlouisfed.org](https://fred.stlouisfed.org).

**Run**

Open `taylore_rule.ipynb` in Jupyter and run all cells.

## Limitations

Standard errors may be unreliable due to autocorrelation in the residuals. 
A HAC-robust estimator (Newey-West) would be more appropriate for inference — 
a planned extension of this project.