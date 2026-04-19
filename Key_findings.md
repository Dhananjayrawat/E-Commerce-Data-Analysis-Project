Key Findings
1. Data Distribution & Quality
Dataset contains 541,909 transactions across multiple countries
Time period: December 2010 - December 2011
Strong right-skewed distribution in quantity and price variables
Data is leptokurtic (high peak with fat tails), indicating presence of extreme values
2. Outlier Analysis
Standard Deviation Distribution:
Within 1 STD: 94.45%
Within 2 STD: 96.45%
Within 3 STD: 98.04%
Outliers found: 9,995 transactions (1.84% of data)
Used cube root transformation to normalize extreme values while preserving negative values
3. Purchase Segregation
Created three categories based on Z-score analysis:
Large Returns: Z-score ≤ -3 (negative orders/refunds)
Regular Purchases: -3 < Z-score < 3 (normal orders)
Large Purchases: Z-score ≥ 3 (bulk orders)
4. Patterns
Clear seasonality visible with peaks during holiday seasons
Consistent purchase patterns throughout the year
Large purchases and returns show distinct patterns from regular transactions
5. Data Cleaning Actions
Removed non-numeric characters from StockCode
Standardized date format (/ to -)
Applied cube root transformation to quantity variable
Implemented percentile-based clipping (1st-99th percentile)
Calculated Z-scores for anomaly detection
Project Structure
6. Libraries Used
pandas: Data manipulation and analysis
numpy: Numerical computations
matplotlib: Visualization
seaborn: Statistical visualization
scipy: Statistical analysis (skewness, kurtosis)
7. Key Techniques
Data Normalization: Cube root transformation for skewed data
Outlier Detection: Z-score method (±3 threshold)
Percentile Clipping: Using 1st and 99th percentiles
Time Series Decomposition: Monthly aggregation and trend analysis
Statistical Measures: Kurtosis, skewness, and standard deviation analysis