# Factor Model Implementation

Fama-French 3-factor and 5-factor models for systematic risk decomposition and alpha analysis.

## Features

- **Fama-French 3-Factor**: Market, Size (SMB), Value (HML) factors
- **Fama-French 5-Factor**: Adds Profitability (RMW) and Investment (CMA)
- **Alpha/Beta Decomposition**: Separate systematic vs idiosyncratic risk
- **Performance Attribution**: Explain returns by factor exposure
- **Rolling Analysis**: Time-varying factor loadings
- **Real Data**: Fetches from Ken French's data library

## Installation

```bash
pip install -r requirements.txt
```

## Quick Start

```python
from ff3_model import analyze_stock

# Analyze any stock's factor exposures
model = analyze_stock('AAPL', period='5y')

# Output:
# Alpha (annualized): 12.34%
# Market Beta: 1.21
# SMB Beta: -0.15 (large-cap tilt)
# HML Beta: -0.45 (growth characteristics)
```

## Modules

| Module | Description |
|--------|-------------|
| `data_loader.py` | Fetch FF factors from Ken French library |
| `ff3_model.py` | Fama-French 3-factor model |
| `ff5_model.py` | Fama-French 5-factor model |
| `alpha_beta.py` | Return/risk decomposition and attribution |
| `visualization.py` | Rolling betas, factor comparison plots |

## Factor Definitions

| Factor | Description | Interpretation |
|--------|-------------|----------------|
| **Mkt-RF** | Market excess return | Systematic market risk |
| **SMB** | Small Minus Big | Size premium (small caps outperform) |
| **HML** | High Minus Low | Value premium (value beats growth) |
| **RMW** | Robust Minus Weak | Profitability premium |
| **CMA** | Conservative Minus Aggressive | Investment premium |

## Mathematical Background

### Factor Model Regression
$$R_i - R_f = \alpha + \beta_{mkt}(R_m - R_f) + \beta_{smb}(SMB) + \beta_{hml}(HML) + \epsilon$$

### Alpha Interpretation
- **α > 0**: Stock outperforms after adjusting for factor exposures (skill)
- **α < 0**: Stock underperforms risk-adjusted benchmark
- **α ≈ 0**: Returns explained by systematic factors

### Risk Decomposition
$$\sigma^2_{total} = \sigma^2_{systematic} + \sigma^2_{idiosyncratic}$$

## Example Output

```
Fama-French 3-Factor Model: AAPL
============================================================

Alpha (annualized): 15.23%
  t-stat: 2.45, p-value: 0.0145 **

Factor Betas:
  Factor       Beta     t-stat    p-value
  Mkt-RF      1.198      45.23     0.0000 ***
  SMB        -0.142      -3.21     0.0014 ***
  HML        -0.523      -8.45     0.0000 ***

R-squared: 0.7234
------------------------------------------------------------
Interpretation:
  • Market Beta=1.20: More volatile than market (aggressive)
  • SMB Beta=-0.14: Large-cap exposure
  • HML Beta=-0.52: Growth stock characteristics
```

## Requirements

- Python 3.8+
- NumPy, Pandas, SciPy
- statsmodels
- Matplotlib
- yfinance, pandas-datareader

## References

- Fama & French (1993): "Common risk factors in stock and bond returns"
- Fama & French (2015): "A five-factor asset pricing model"

## License

MIT
