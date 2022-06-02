<img src= "images/fraud.png" width="930" height="300">

# Credit Risk Classification

With over 200 million users, MercadoLibre is the most popular e-commerce site in Latin America. This notebook analyzes the company's financial and user time series data in order to predict if search traffic can translate into the ability to successfully trade the stock.

Specifically, the notebook includes depictions of seasonality (as measured by Google Search traffic), evaluates how the company’s stock price correlates to its Google Search traffic, and uses forecast models to predict hourly user search traffic and revenues.

---

## Technologies

This application leverages python 3.7 with the following packages that require additional installation:

* pandas: an open-source library that offers easy-to-use data analysis tools for Python.
* fbprophet: FbProphet is a powerful time series analysis package released by Core Data Science Team at Facebook.
* hvplot: hvPlot provides a high-level plotting API built on HoloViews that provides a general and consistent API for plotting data.
* holoviews: a Python library designed to make data analysis and visualization seamless and simple.
* matplotlib: a comprehensive library for creating static, animated, and interactive visualizations in Python.

---

## Installation Guide

Begin by cloning the GitHub repo (the same repo that this README.md file is contained within) into your terminal. 

Because this code uses [Facebook Prophet library](https://facebook.github.io/prophet/), which can be difficult to install on some machines, we recommend using the Google Colab IDE. Google Colab allows you to run Jupyter Notebooks in the cloud. By installing libraries within Google Colab instead of onto your machine, you are installing them only temporarily, in memory, while using the cloud. 

To configure a [Google Colab](https://colab.research.google.com/) workspace:

* Open Google Colab and upload the notebook contained within this repo.

* Run the provided code in the notebook's install section and import the required libraries and dependencies in the following section.

---

## Usage

**Part 1: Find Unusual Patterns in Hourly Google Search Traffic**

This section investigates whether the Google search traffic for the company links to any financial events at the company by selecting unusual patterns in the Google search data for the company and connecting them to the corporate financial events.

To do so, the code reads the search data into a DataFrame, and then slices the data to just the month of May 2020 (during this month, MercadoLibre released its quarterly financial results). Using hvPlot to visualize the results, any notable patterns are identified. 

Next, the total search traffic for the month is calculated and then compared to the monthly median across all months. 

**Part 2: Mine the Search Traffic Data for Seasonality**

This section tracks and predicts interest in the company and its platform for any time of day, permitting the marketing team to focus their efforts around the times that have the most traffic in order to achieve greater return on investment.

In pursuit of this goal, the code mines the search traffic data for predictable seasonal patterns of interest in the company by first collecting the hourly search data and plotting it by day-of-the-week. Visualizing this traffic as a heatmap, referencing the index.hour as the x-axis and the index.dayofweek as the y-axis, the user is able to view day-of-week effects and their concentration over the course of the day.

Next, the search data is grouped by the week-of-the-year to depict weekly patterns across the calendar year.

**Part 3: Relate the Search Traffic to Stock Price Patterns**

This section investigates whether any relationship between the search data and the company stock price exists.

To do so, the code first reads in and plots the stock price data then concatenates the stock price data to the search data in a single DataFrame. 

Next, the code slices the data to just the first half of 2020 (2020-01 to 2020-06), and then use hvPlot to plot the data.

A new column in the DataFrame is then created named “Lagged Search Trends” that offsets, or shifts, the search traffic by one hour, along with two additional columns: “Stock Volatility”, which holds an exponentially weighted four-hour rolling average of the company’s stock volatility, and “Hourly Stock Return”, which holds the percent change of the company's stock price on an hourly basis.

The time series correlations are then reviewed, and any predictable relationships existing between the lagged search traffic and the stock volatility or between the lagged search traffic and the stock price returns are noted.

**Part 4: Create a Time Series Model with Prophet**

In this section, a time series model that analyzes and forecasts patterns in the hourly search data is created using Prophet. 

After estimating the model, the forecast is plotted, along with the individual time series components of the model to depict which time of day exhibits the greatest popularity, which day of the week gets the most search traffic, and what the lowest point for search traffic is in the calendar year.

**Part 5: Forecast Revenue by Using Time Series Models**

This section generates a forecast of the total sales for the next quarter.

The daily historical revenue figures are read-in, and then a Prophet model is applied to the data and the forecast for the next quarter is plotted (as shown here).

![Revenue forecast example.](images/revenueforecast.png)

The model's output is interpreted to identify any patterns in the company's revenue, specifically which are the peak revenue days.

A sales forecast for the finance group is finally produced including a number for the expected total sales in the next quarter along with the best- and worst-case scenarios to help MercadoLibre plan accordingly.

---

## Contributors

Nicole Roberts,
elle.nicole.roberts@gmail.com

---

## License

[BSD 3](https://choosealicense.com/licenses/bsd-3-clause-clear/): BSD 3-clause is a permissive licence, allowing nearly unlimited freedom with the software as long as BSD copyright and license notice is included.