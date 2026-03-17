1. Project Overview
This project aims to automate the processing of global COVID-19 data to extract meaningful trends and provide a 7-day forecast for both Global and Regional (India) confirmed cases. The pipeline handles data cleaning, time-series aggregation, and predictive modeling.
2. Data Processing Pipeline
The script performs the following transformations:

Normalization: Column names are stripped of whitespace and special characters (/,  ) to ensure compatibility with Python's dot notation.

Type Casting: The Date column is parsed into datetime64 objects, and metric columns (Confirmed, Deaths, Recovered, Active) are forced to integers.

Aggregation: Data is grouped by Date for global trends and by Country for snapshot comparisons.
3. Exploratory Data Analysis (EDA)
The analysis generates several key visualizations to understand the pandemic's trajectory:

3.1 Global Trends
A multi-line chart tracks the divergence between Confirmed, Recovered, and Death cases.

3.2 Geographic Distribution
A Choropleth Map is generated using Plotly to visualize the density of confirmed cases across the globe. This allows for immediate identification of "hotspots" at the latest available data point.
4. Forecasting MethodologyThe project employs a dual-layered forecasting approach to ensure reliability even if specific libraries are missing.
4.1 The Prophet Model (Primary)If available, the Facebook Prophet library is used. It treats the time series as an additive model:$$y(t) = g(t) + s(t) + h(t) + \epsilon_t$$$g(t)$: Trend function (modeled as piecewise linear).$s(t)$: Periodic changes (weekly seasonality to account for lower reporting on weekends).$\epsilon_t$: Error term representing idiosyncratic changes.4.2 Simple Moving Average (Fallback)If Prophet is unavailable, the script calculates the 7-day average of new cases and projects that growth linearly into the future. This provides a "naive" but grounded estimate based on the most recent momentum.
5. Key Outputs
The script saves all results into the covid_analysis_outputs directory:

top10_countries_latest.csv: A summary of the hardest-hit regions.

global_time_series.html: An interactive dashboard for deep-diving into specific dates.

global_confirmed_forecast.csv: The predicted values for the upcoming week.
6. Conclusion
By combining historical data visualization with time-series forecasting, this tool provides a comprehensive view of the pandemic's status. The modular nature of the code allows for easy adaptation to other infectious disease datasets.
