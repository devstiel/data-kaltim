# Time Series Forecasting for East Kalimantan Price Data: A Comparative Study of ARIMA and Hybrid ARIMA-LSTM Models

## Abstract

This research presents a comprehensive time series analysis and forecasting study of commodity price data from East Kalimantan, Indonesia. The study implements and compares traditional ARIMA (AutoRegressive Integrated Moving Average) models with hybrid ARIMA-LSTM (Long Short-Term Memory) approaches to forecast price movements. Multiple train-test split scenarios (80-20, 70-30, 60-40) are evaluated to assess model robustness and generalization capabilities across different data distributions.

## Keywords
Time Series Forecasting, ARIMA, LSTM, Hybrid Models, Price Prediction, East Kalimantan, Indonesia, Statistical Modeling

## 1. Introduction

Time series forecasting plays a crucial role in economic analysis and market prediction. This study focuses on commodity price forecasting using historical data from East Kalimantan (Kaltim), Indonesia, spanning from January 2021 to August 2024. The research compares the performance of traditional statistical methods (ARIMA) with modern deep learning approaches (LSTM) and their hybrid combinations.

### 1.1 Research Objectives
- Compare the forecasting accuracy of ARIMA and hybrid ARIMA-LSTM models
- Evaluate model performance across multiple train-test split scenarios
- Identify optimal parameters for time series forecasting of East Kalimantan price data
- Assess the effectiveness of hybrid approaches in improving forecast accuracy

## 2. Dataset Description

**Dataset**: East Kalimantan Price Data (`datakaltim.csv`)
- **Time Period**: January 1, 2021 - August 30, 2024
- **Frequency**: Daily observations
- **Total Observations**: 1,338 data points
- **Variables**: 
  - `Tanggal` (Date): Daily timestamps in DD/MM/YYYY format
  - `Harga (Rp)` (Price in Rupiah): Daily price values ranging from 11,200 to 16,900 IDR

### 2.1 Data Characteristics
- **Price Range**: 11,200 - 16,900 Indonesian Rupiah
- **Data Quality**: Complete time series with no missing values
- **Trend**: Generally upward trend with periodic fluctuations
- **Volatility**: Moderate price volatility with occasional spikes

## 3. Methodology

### 3.1 Data Preprocessing
1. **Date Conversion**: Convert date strings to datetime objects
2. **Data Cleaning**: Remove comma separators from price values and convert to numeric
3. **Index Setting**: Set date as the primary index for time series analysis
4. **Stationarity Testing**: Apply Augmented Dickey-Fuller (ADF) test
5. **Differencing**: First-order differencing to achieve stationarity

### 3.2 Exploratory Data Analysis (EDA)
- Time series visualization and trend analysis
- Statistical summaries and distribution analysis
- Autocorrelation Function (ACF) and Partial Autocorrelation Function (PACF) plots
- Stationarity assessment using ADF test

### 3.3 Model Development

#### 3.3.1 ARIMA Model Implementation
- **Parameter Optimization**: Grid search over p and q values
- **Parameter Range**: p ∈ {1, 2, 3, 4, 6, 7, 8, 9, 10, 12, 18}, q ∈ {1, 3, 6, 20}
- **Differencing Order**: d = 2 (determined through stationarity testing)
- **Model Selection**: Based on Mean Squared Error (MSE) and Mean Absolute Percentage Error (MAPE)

#### 3.3.2 Hybrid ARIMA-LSTM Model
- **ARIMA Component**: Captures linear trends and seasonal patterns
- **LSTM Component**: Models residuals from ARIMA to capture non-linear patterns
- **Architecture**: 60-day lookback window for LSTM training
- **Residual Modeling**: LSTM trained on ARIMA residuals to capture remaining patterns

### 3.4 Evaluation Framework

#### 3.4.1 Train-Test Split Scenarios
1. **80-20 Split**: 1,070 training, 268 testing observations
2. **70-30 Split**: 936 training, 402 testing observations  
3. **60-40 Split**: 802 training, 536 testing observations

#### 3.4.2 Performance Metrics
- **Mean Squared Error (MSE)**: Measures average squared prediction errors
- **Mean Absolute Error (MAE)**: Average absolute prediction errors
- **Mean Absolute Percentage Error (MAPE)**: Percentage-based error metric
- **R-squared (R²)**: Coefficient of determination for goodness of fit

## 4. Results

### 4.1 ARIMA Model Performance

#### 4.1.1 Optimal Parameters
- **80-20 Split**: ARIMA(8, 2, 20) - MSE: 143,437.54, MAPE: 1.78%, R²: 46.88%
- **70-30 Split**: ARIMA(6, 2, 6) - MSE: 199,584.57, MAPE: 2.12%, R²: 62.54%
- **60-40 Split**: ARIMA(10, 2, 1) - MSE: 158,836.36, MAPE: 2.09%, R²: 82.14%

#### 4.1.2 Best Performing Models
- **Best by MSE**: ARIMA(9, 2, 3) with MSE: 143,060.80
- **Best by MAPE**: ARIMA(8, 2, 20) with MAPE: 1.78%

### 4.2 Hybrid ARIMA-LSTM Performance

#### 4.2.1 Model Results by Split
- **80-20 Hybrid**: MSE: 49,426.69, MAPE: 1.06%, R²: 57.24%
- **70-30 Hybrid**: MSE: 55,117.07, MAPE: 1.14%, R²: 52.31%
- **60-40 Hybrid**: Performance metrics vary based on LSTM architecture

### 4.3 Comparative Analysis
- **Hybrid Models** consistently outperform standalone ARIMA models
- **MAPE Improvement**: Hybrid models achieve 40-50% lower MAPE values
- **MSE Reduction**: Significant MSE reduction in hybrid approaches
- **R² Enhancement**: Better explanatory power in hybrid models

## 5. Model Implementation Details

### 5.1 Software and Libraries
- **Python 3.x** for implementation
- **pandas** for data manipulation
- **NumPy** for numerical computations
- **matplotlib/seaborn** for visualization
- **statsmodels** for ARIMA implementation
- **TensorFlow/Keras** for LSTM neural networks
- **scikit-learn** for evaluation metrics

### 5.2 Computational Requirements
- Standard desktop/laptop configuration sufficient
- GPU acceleration optional for LSTM training
- Memory requirements: <4GB RAM for dataset size

## 6. Project Structure

```
ARIMA/
├── ARIMA_dan_Hybrid.ipynb    # Main analysis notebook
├── datakaltim.csv            # East Kalimantan price dataset
├── Readme.md                 # Project documentation
└── arima80.csv              # Forecast results (generated)
```

## 7. Usage Instructions

### 7.1 Prerequisites
```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels tensorflow
```

### 7.2 Running the Analysis
1. Open `ARIMA_dan_Hybrid.ipynb` in Jupyter Notebook/Lab
2. Execute cells sequentially for complete analysis
3. Modify parameters as needed for experimentation
4. Review generated visualizations and metrics

## 8. Key Findings

### 8.1 Model Performance Hierarchy
1. **Hybrid ARIMA-LSTM**: Best overall performance
2. **Optimized ARIMA**: Good baseline with proper parameter tuning
3. **Standard ARIMA**: Adequate but suboptimal without optimization

### 8.2 Split Scenario Insights
- **60-40 Split**: Highest R² values but limited training data
- **80-20 Split**: Balanced performance with sufficient training data
- **70-30 Split**: Moderate performance across all metrics

### 8.3 Practical Implications
- Hybrid models provide superior forecasting accuracy
- Parameter optimization crucial for ARIMA performance
- Daily price forecasting feasible with developed models
- Methodology applicable to other Indonesian commodity markets

## 9. Limitations and Future Work

### 9.1 Current Limitations
- Single commodity focus (East Kalimantan specific)
- Limited to daily frequency data
- No external factor integration (seasonality, economic indicators)
- Computational complexity of hybrid models

### 9.2 Future Research Directions
- Multi-variate time series analysis
- Integration of external economic indicators
- Real-time forecasting system development
- Extended evaluation on other Indonesian regional data
- Advanced deep learning architectures (Transformer models)

## 10. Contact Information

**Author**: Dia Naufal Abiyyu Tsaqif, Devy Relliani Saffiyah, Luthfan Aryananda Purwito
**Institution**: Insititut Teknologi Sepuluh Nopember 
**Course**: Pemodelan Analitika Preskriptif 1 
**Academic Year**: 2024/2025

---

*This project is submitted as part of academic coursework in time series analysis and forecasting methodologies.*