## Dataset

- **Monthly Beer Production** (1956–1973)  
- Stored in `data/beer_production.csv`  
- Columns:  
  - `Month` – timestamp (YYYY-MM-DD)  
  - `Monthly beer production` – production volume  

---

## Time Series Analysis Concepts

- **Time Domain Analysis:** looks at the series chronologically, identifies trends and seasonality  
- **Autocorrelation Function (ACF):** correlation of residuals with past values  
- **Partial Autocorrelation Function (PACF):** direct correlation at each lag after removing intermediate effects  

---

## Decomposition

We use **multiplicative decomposition** to separate the series into:

\[
Y_t = T_t \times S_t \times R_t
\]

Where:  

- **Trend (Tₜ):** long-term movement in production  
- **Seasonal (Sₜ):** repeating yearly patterns  
- **Residual (Rₜ):** random noise  

---

### Variance Structure: Additive vs Multiplicative

- Seasonal fluctuations **increase as production grows**, indicating multiplicative behavior  
- **Coefficient of Variation (CV):** 0.247 → moderate variability  
- **Rolling variance** shows slight increase → multiplicative decomposition is appropriate  

---

### Choice of Decomposition Model

> Because the magnitude of seasonal fluctuations grows with production, we choose a **multiplicative decomposition model**.

---

