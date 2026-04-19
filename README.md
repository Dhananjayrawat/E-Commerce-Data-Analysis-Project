# E-Commerce Data Analysis Project 
This project analyzes e-commerce transaction data to identify purchasing patterns, detect anomalies, and segment customer behavior based on quantity transactions. The analysis includes statistical distribution analysis, outlier detection, and time-series visualization.
## Overview
Comprehensive analysis of e-commerce transaction data with focus on:
- Outlier detection and handling
- Customer segmentation based on order quantity
- Temporal trend analysis
- Statistical distribution analysis

## Data Processing
- Removed non-numeric characters from product codes
- Standardized date formats
- Applied cube root transformation to reduce outlier impact
- Clipped data to 1st-99th percentile

## Key Metrics
- 541,909 transactions analyzed
- 9,995 outliers detected
- ~94% of data within 1 standard deviation after cleaning

## Installation
pip install pandas numpy seaborn matplotlib

## Usage
python analysis.py

## Project Structure