# AeroSense AI: Intelligent Air Quality Forecasting Through Spatiotemporal Learning and Cross-Station Generalization

## Overview
A multi-station PM2.5 forecasting research project using historical air-quality observations from Beijing, China.

## Objectives
- Forecast PM2.5 at 1-hour, 6-hour and 24-hour horizons.
- Evaluate cross-station generalization using Leave-One-Station-Out (LOSO).
- Compare GRU and LSTM models.
- Explore pretrained time-series foundation-model forecasting and LoRA fine-tuning.

## Dataset
Beijing Multi-Site Air Quality Dataset
- Source: UCI Machine Learning Repository
- Period: March 2013 – February 2017
- Stations: 12
- Observations: 420,768
- Target: PM2.5

Citation: Chen, S. (2017). Beijing Multi-Site Air Quality. UCI Machine Learning Repository.
https://doi.org/10.24432/C5RK5G

The dataset is not included in this repository.

## Neural LOSO Results

| Model | Horizon | MAE | RMSE | R2 |
|---|---:|---:|---:|---:|
| GRU | 1 hour | 10.1248 | 19.4704 | 0.9544 |
| GRU | 6 hours | 33.9258 | 56.6961 | 0.6178 |
| GRU | 24 hours | 58.1233 | 86.7567 | 0.1049 |
| LSTM | 1 hour | 10.3225 | 19.8405 | 0.9526 |
| LSTM | 6 hours | 34.6609 | 58.2361 | 0.5973 |
| LSTM | 24 hours | 57.9661 | 87.4383 | 0.0936 |

Results are means across 12 held-out stations.

## Foundation-Model Pilot

Single-station pilot at Aotizhongxin, using 18 test windows.

| Model | Horizon | MAE | RMSE | R2 |
|---|---:|---:|---:|---:|
| Pretrained | 1 hour | 20.2012 | 32.0295 | 0.9188 |
| LoRA | 1 hour | 18.8463 | 29.8176 | 0.9296 |
| Pretrained | 6 hours | 32.2498 | 44.7551 | 0.8350 |
| LoRA | 6 hours | 34.5886 | 50.3961 | 0.7908 |
| Pretrained | 24 hours | 40.3413 | 56.6565 | 0.7765 |
| LoRA | 24 hours | 39.0310 | 55.9553 | 0.7820 |

LoRA improved the 1-hour and 24-hour results but not the 6-hour result. This pilot is not directly comparable to the multi-station neural LOSO results.

## Evaluation Metrics
- MAE: Mean Absolute Error
- RMSE: Root Mean Squared Error
- R2: Coefficient of Determination

## Limitations
- Foundation-model evaluation is limited to one station.
- Only 4 of 36 planned corrected ExtraTrees experiments are available.
- Performance decreases at longer forecasting horizons.

## Future Work
- Complete baseline experiments.
- Evaluate foundation models across all stations.
- Explore spatial information and uncertainty estimation.

## Author
Independent AI and machine-learning research project.
