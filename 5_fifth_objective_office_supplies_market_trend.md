# Objective 5 - Office Supplies Market Trend Analysis and Forecast
To analyze the trend in the Office Supplies market and provide a forecast for the upcoming year (2015), a Databricks notebook named ["3_Trend_and_Forecast.ipynb"](https://github.com/Prof-MatheusAndrade/Sales-Dataset-Exploration/blob/main/0_Materials/2_Databricks_Notebooks/3_Trend_and_Forecast.ipynb) was employed for the analysis. The notebook documents all the steps involved in the investigation. was employed for the analysis. The notebook details all the steps involved in the investigation.

## Data Analysis and Trend Calculation
In the first step, a SQL query was utilized to summarize the total sales by Order Date, combining the fact table "Order" with dimension tables "Product," "Product_Category," and "Calendar_Date."

After obtaining the data, Plotly and Pandas were used to generate visualizations. The first plot is a histogram depicting the number of orders by each month, showcasing a balanced distribution.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14IOPDhNH0alYvNmzEhRV3_Acc0b1Zc-n"  width="80%" height="40%">
</p>

The second plot is a line plot illustrating sales results by each month. The plot reveals an increase in the last months, with a smooth upward trend over the years.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14KGAEU5LpTcHOL0NelJeJ8QXHPADYtW0"  width="80%" height="40%">
</p>

The third plot, calculated by Ordinary Least Squares (OLS) regression, provides a Sales Trend view, making it clearer to observe the sales increase in the last years. Ordinary Least Squares (OLS) regression is a statistical technique used to estimate the parameters of a linear regression model by minimizing the sum of squared differences between observed and predicted values. In the context of trend analysis, OLS regression helps quantify the relationship between a dependent variable, such as sales in this case, and independent variables, providing a linear equation that best fits the observed data and facilitates the understanding of trends over time.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14WpewRqaVncuhiOEUxJiJ6njCEWO5cXG"  width="80%" height="40%">
</p>

The fourth plot, also representing the Sales Trend, is calculated by a Moving Average with a window size of 3 months, displaying an increase with some seasonalities during the years.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14csgnU0loUYa1E5jBOP4zf3w20i_QXdE"  width="80%" height="40%">
</p>

## Forecast
The forecast preparation began using the PyCaret library. The "setup" function was employed, utilizing the timeseries dataset and choosing a test data size of 10 months out of the total 48 months. The figure below shows the "setup" process results.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14ih6f3eaIEA9EOkr3lkS9HHL5qtjH7MW"  width="60%" height="30%">
</p>

Next, the analysis involved comparing results between different timeseries models, using key metrics such as MAE (Mean Absolute Error) and RMSE (Root Mean Squared Error). Comparing results are presented in the figure below.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14kvreKVDjI8IxLYfLIfaFnfWJSdKZnA_"  width="80%" height="40%">
</p>

Based on the comparison, the Seasonal Naive Forecaster ("snaive") emerged as the best model. A Seasonal Naive Forecaster is a method that predicts future values based on the observed values from the corresponding season in previous years. Subsequently, the model underwent tuning, selecting the Mean Absolute Error (MAE) as the optimization criterion to minimize forecast errors. The figure below displays the forecast results for the test data, revealing a range of error in the predictions. Despite this, the model appears to adeptly capture the underlying behavior of the time series data.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14fVd_bx026y0JjjDGmEoyzilhOjsdJDK"  width="80%" height="40%">
</p>

The final forecast for the next year (2015) using the tuned model is presented below. While there is a range of error in the prediction, the forecast indicates a similar behavior in the upcoming year, possibly with a small increase or decrease.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=14gEyGqTp_viO3tEyNplDWHFrDUCtMxVr"  width="80%" height="40%">
</p>
