# Time_Series_Analysis Introduction

---

## What is a Time Series?

Time series analysis is a collection of observations made sequentially over time

---

## **Example of time series**

a) ****Economic and financial time series****

- This includes exports totals recorded in succssive years,sales recorded monthly,share prices recorded in successive days

b) **Marketing time series**

- This includes advertising costs on successive years,revenue in successive days

c) **Physical series**

- Deals with physical sciences,marine sciences and geo physics eg rainfall amts in successive days,temperatur recorded daily

d) **Demographic time series**

-This deals with popultion metrics e.g total population recorded yearly,birth and death totals recorded monthly.This is useful to governments a they are able to make decisions and  put measures in place to support the people

```

- N/B: Apart from these we have process cotrol data,binary processes,and point processes

```
---

## Roles of Time Series Analysis

Time series analysis plays several important roles:

1. **Understanding Patterns**
   - Identify trends and seasonal effects
   - Discover hidden structures in data

2. **Explanation**
   - Explain why a variable behaves the way it does over time

3. **Monitoring**
   - Detect abnormal behavior or sudden changes

4. **Forecasting**
   - Predict future values based on historical patterns

5. **Decision Support**
   - Help organizations plan and allocate resources efficiently

---

## Objectives of Time Series Analysis

The main objectives are:

- To describe the data
- To model the data-generating process
- To separate different components of variation
- To make accurate predictions
- To quantify uncertainty

---

## Approaches to Time Series Analysis

There are two broad approaches to analyzing time series data:

### 1. Time Domain Analysis
Time domain analysis focuses on the **temporal order of observations**.  
It studies patterns as they occur over time.

Common techniques:
- **Plotting & Visualization** – Identify trends, seasonality, and anomalies
- **Smoothing & Moving Averages** – Reduce noise to highlight patterns
- **Autocorrelation & Partial Autocorrelation** – Measure correlation of the series with its past values
- **Decomposition** – Break a series into trend, seasonal, and residual components
- **Time Domain Modeling** – AR, MA, ARMA, ARIMA models

Time domain analysis is widely used for forecasting and understanding **how past values influence the present**.

---

### 2. Frequency Domain Analysis
Frequency domain analysis focuses on **cyclical behavior** and **periodic patterns** in a series by converting it from the time domain into the frequency domain.

Common techniques:
- **Fourier Transform** – Decompose a series into sinusoidal components
- **Spectral Analysis** – Identify dominant cycles and periodicities
- **Filtering** – Extract specific frequency components (e.g., seasonal cycles)
- **Wavelet Analysis** – Study localized time-frequency patterns

Frequency domain analysis is especially useful when:
- There are multiple overlapping cycles
- Seasonality is not obvious
- We want to isolate high-frequency noise from low-frequency trends

---

### Summary
- **Time Domain:** Directly studies observations over time; easier to visualize; foundational for most classical methods.  
- **Frequency Domain:** Studies patterns as combinations of cycles; powerful for detecting hidden periodicities and complex seasonality.

---

## Time Series Decomposition

**Decomposition** is the process of splitting a time series into:
- Trend
- Seasonal
- Residual components

It helps to:
- Understand underlying patterns
- Decide which model to use
- Compare different datasets
- Prepare data for forecasting

In this repository, decomposition is treated as a **core topic**, and it is applied to multiple datasets to show how the same technique reveals different behaviors in different domains.We work on a beer production dataset

---

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

## Autocorrelation and Partial Autocorrelation (ACF & PACF) Analysis

Autocorrelation and partial autocorrelation are essential tools in time series analysis for understanding relationships between observations at different lags. They help identify **trend**, **seasonality**, and **stationarity** of the series.  

### Interpretation of ACF and PACF – Original Series

From the ACF plot of the original series, we observe that:

- The autocorrelations are large and positive for many lags.  
- The ACF decays very slowly rather than cutting off quickly.  
- Significant spikes appear at seasonal lags (e.g., around lag 12 and 24).

This slow decay pattern indicates that the series is **non-stationary**, likely due to the presence of a trend and/or seasonality.

From the PACF plot:

- There is a strong spike at lag 1.  
- Additional significant spikes appear at seasonal lags.  
- The PACF does not show a sharp cutoff after a small number of lags.

**Conclusion:**  
The original beer production series is not stationary, as evidenced by:

- Slow decay in the ACF  
- Multiple significant autocorrelations across many lags  
- Clear seasonal structure  

Therefore, **differencing is required before fitting an ARIMA model**.

---

### Interpretation of ACF and PACF – Differenced Series

After applying first differencing, the autocorrelation structure changes significantly.

#### ACF Observations:

- The slow decay observed in the original series is no longer present.  
- Most autocorrelations now fall within the confidence bounds.  
- A significant spike remains at lag 12, indicating seasonal dependence.  
- A few small negative spikes appear at early lags, but they decay quickly.

This suggests that first differencing has successfully removed the **trend component** and improved stationarity.

#### PACF Observations:

- The strong persistence seen in the original series is no longer present.  
- Several negative spikes appear at early lags.  
- A noticeable seasonal effect is visible around lag 12.  
- There is no clear sharp cutoff at a small lag.

**Conclusion:**  
The series appears much closer to stationarity after first differencing.  

- The significant spike at lag 12 in the ACF indicates **remaining seasonal structure**.  
- Seasonal differencing may be required.  
- A **Seasonal ARIMA (SARIMA) model** is likely appropriate.

---

### Interpretation of ACF and PACF – Seasonal Differenced Series (Lag 12)

After applying seasonal differencing at lag 12, the strong seasonal spike observed in the original ACF has been substantially reduced.

#### ACF Observations:

- The large seasonal persistence at lag 12 is no longer dominant.  
- Most autocorrelations fall within the confidence bounds.  
- A few small spikes remain at early lags.  
- No slow decay pattern is visible.

#### PACF Observations:

- No strong or systematic cutoff pattern is visible.  
- Most spikes lie within confidence bounds.  
- A moderate negative spike appears at lag 12.

**Conclusion:**  
Seasonal differencing has effectively removed the annual pattern.  

- If a trend was also present, **both first differencing and seasonal differencing** may be required before fitting a SARIMA model.

---

### Interpretation of ACF and PACF – Double Differenced Series

#### ACF Analysis:

- Most autocorrelations lie within the 95% confidence bounds.  
- No slow decay pattern is visible.  
- No strong repeating seasonal spike remains at lag 12.  
- Autocorrelations fluctuate randomly around zero.

#### PACF Analysis:

- No sharp cutoff at early lags.  
- No dominant AR structure.  
- Most partial autocorrelations fall within the confidence interval.  
- No systematic seasonal AR pattern remains.

#### Stationarity Assessment:

The absence of:

- Persistent autocorrelation  
- Seasonal spikes  
- Slow decay patterns  

indicates that the transformed series is likely **covariance-stationary**.

#### Implication for Modeling:

Since the double-differenced series resembles white noise:

- Only small AR or MA terms may be required.  
- Overfitting should be avoided.  
- A **parsimonious SARIMA model** is preferred.

A reasonable starting point would be:

```text
SARIMA(p,1,q)(P,1,Q)12
```
