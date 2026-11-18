# AeroSense AI
## Intelligent Air Quality Forecasting Through Spatiotemporal Learning and Cross-Station Generalization

### Abstract

Air quality forecasting is important for understanding pollution dynamics
and supporting environmental monitoring. This project investigates
machine-learning and deep-learning approaches for forecasting PM2.5
concentrations across multiple monitoring stations.

Using the Beijing Multi-Site Air Quality dataset, the study evaluates
LSTM and GRU models through leave-one-station-out (LOSO) experiments.
A TimesFM 2.5 experiment is also included as an exploratory single-station
pilot. Corrected ExtraTrees experiments are retained as partial results.

The neural experiments provide a multi-station evaluation across 12
stations and three forecast horizons. Results indicate that short-term
forecasting is substantially more accurate than longer-horizon forecasting.
The project also documents limitations in the completeness and comparability
of the additional model experiments.

### 1. Introduction

Air pollution is a major environmental concern. PM2.5 forecasting is
challenging because pollutant concentrations vary over time and across
geographical monitoring locations.

A model trained at one station may not generalize equally well to another
station. This project therefore investigates forecasting performance
under a cross-station evaluation setting rather than relying only on
randomly selected observations from a single location.

### 2. Objectives

- Study hourly air-quality observations from multiple monitoring stations.
- Forecast PM2.5 at 1-hour, 6-hour, and 24-hour horizons.
- Evaluate LSTM and GRU models using leave-one-station-out experiments.
- Explore a time-series foundation model through a TimesFM 2.5 pilot.
- Retain corrected ExtraTrees experiments while clearly reporting
  their incomplete coverage.
- Compare forecasting errors using MAE, RMSE, and R².

### 3. Dataset

The project uses the Beijing Multi-Site Air Quality dataset from the
UCI Machine Learning Repository.

- Observations: 420,768
- Monitoring stations: 12
- Time span: March 2013 to February 2017
- Sampling frequency: Hourly
- Target variable: PM2.5

The dataset contains pollutant measurements and meteorological variables,
including PM10, SO2, NO2, CO, O3, temperature, pressure, dew point,
rainfall, wind direction, and wind speed.

Dataset reference:

Chen, S. (2017). Beijing Multi-Site Air Quality [Dataset].
UCI Machine Learning Repository.
https://doi.org/10.24432/C5RK5G

### 4. Experimental Design

#### 4.1 Cross-station evaluation

The principal neural evaluation uses a leave-one-station-out (LOSO)
setting across 12 monitoring stations. Each station is treated as a
held-out evaluation location in turn.

The neural results cover:
- LSTM
- GRU
- 1-hour, 6-hour, and 24-hour forecast horizons

The consolidated neural results contain 72 station-level records:
12 stations × 2 architectures × 3 forecast horizons.

#### 4.2 Evaluation metrics

The experiments use:

- **MAE:** Mean Absolute Error, measuring average absolute prediction error.
- **RMSE:** Root Mean Squared Error, giving greater weight to large errors.
- **R²:** Coefficient of determination, measuring explained variation.

Lower MAE and RMSE indicate smaller errors. Higher R² indicates
better explanatory performance.

### 5. Neural Model Results

The following table reports the aggregate LOSO results across the
12 monitoring stations.

| Model | Horizon | MAE | RMSE | R² |
|---|---:|---:|---:|---:|
| GRU | 1 hour | 10.125 | 19.470 | 0.9544 |
| LSTM | 1 hour | 10.322 | 19.840 | 0.9526 |
| GRU | 6 hours | 33.926 | 56.696 | 0.6178 |
| LSTM | 6 hours | 34.661 | 58.236 | 0.5973 |
| GRU | 24 hours | 58.123 | 86.757 | 0.1049 |
| LSTM | 24 hours | 57.966 | 87.438 | 0.0936 |

#### 5.1 Interpretation

At the 1-hour horizon, GRU achieves an aggregate MAE of approximately
10.125 and an R² of 0.9544. LSTM produces similar performance, with
an MAE of approximately 10.322 and an R² of 0.9526.

At 6 hours, both models show higher errors and lower R² values.
At 24 hours, forecasting becomes substantially more difficult, with
R² values close to 0.10.

These results show a clear reduction in predictive performance as
the forecast horizon increases. GRU performs better on the reported
aggregate MAE and RMSE at the 1-hour and 6-hour horizons, while LSTM
has a marginally lower MAE at 24 hours.

### 6. TimesFM 2.5 Exploratory Pilot

A separate exploratory experiment evaluates TimesFM 2.5 on the
Aotizhongxin station using univariate PM2.5 observations.

The pilot uses:
- Context length: 512
- Forecast horizon: 24
- Test windows: 18
- Validation windows: 5
- Fine-tuning epochs: 3
- LoRA trainable parameters: 1,382,912

#### 6.1 Pretrained and fine-tuned results

| Configuration | Horizon | MAE | RMSE | R² |
|---|---:|---:|---:|---:|
| Pretrained | 1 hour | 20.201 | 32.029 | 0.9188 |
| Fine-tuned | 1 hour | 18.846 | 29.818 | 0.9296 |
| Pretrained | 6 hours | 32.250 | 44.755 | 0.8350 |
| Fine-tuned | 6 hours | 34.589 | 50.396 | 0.7908 |
| Pretrained | 24 hours | 40.341 | 56.657 | 0.7765 |
| Fine-tuned | 24 hours | 39.031 | 55.955 | 0.7820 |

Fine-tuning improves the reported 1-hour and 24-hour pilot metrics,
but does not improve the 6-hour metrics.

**Important limitation:** This is a small single-station pilot with
only 18 test windows and 5 validation windows. It is exploratory
and must not be interpreted as a directly comparable multi-station
benchmark against the LSTM and GRU LOSO results.

### 7. Corrected ExtraTrees Experiments

Corrected ExtraTrees result files are included for four experiments:

- Aotizhongxin — 1 hour
- Wanshouxigong — 1 hour
- Wanshouxigong — 6 hours
- Wanshouxigong — 24 hours

The planned evaluation covered 36 station-horizon combinations.
Only four corrected experiment outputs are currently available.

Consequently, ExtraTrees results are reported as partial experiments
and are not presented as a complete 12-station benchmark. Earlier
results affected by a target-imputation issue are excluded from the
validated publication results.

### 8. Limitations

1. The TimesFM experiment is a small pilot on one station and has
   limited test coverage.
2. The corrected ExtraTrees experiments cover only four of the
   planned 36 station-horizon combinations.
3. TimesFM pilot metrics and multi-station neural LOSO metrics use
   different evaluation settings and should not be compared as if
   they were produced under an identical protocol.
4. Performance decreases considerably at longer forecast horizons.
5. The reported results describe the available experiments and do
   not establish universal performance across other cities or datasets.

### 9. Conclusion

This project investigates multi-station PM2.5 forecasting using
recurrent neural networks and exploratory time-series foundation-model
experiments.

The 12-station LOSO evaluation shows that GRU and LSTM achieve strong
short-term forecasting performance, while accuracy decreases at
longer forecast horizons. The TimesFM 2.5 pilot demonstrates the
feasibility of a parameter-efficient fine-tuning experiment, although
its small test set limits broader conclusions.

The corrected ExtraTrees experiments are retained transparently as
partial results. Overall, the project provides an experimental
framework for studying temporal forecasting and cross-station
generalization in air-quality data.

### 10. Repository Contents

The accompanying repository contains:
- Cleaned research notebooks
- Consolidated neural LOSO result files
- TimesFM pilot metrics, predictions, and training history
- Partial corrected ExtraTrees results
- Final comparison figures
- This research report
