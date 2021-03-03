# Improving weather forecasts with BigQuery ML

## TL;DR
* Numerical weather prediction (using computer models to aid in weather forecasting) has a rich history of using statistical methods to improve forecasts.
* Google Cloud BigQuery provides (as of March 2021) easy access to more than two dozen weather- and climate-related datasets.
* Using these publicly available datasets, you can set up a machine learning model to improve weather forecasts for anywhere in the world, all using SQL within BigQuery.

## Introduction

## Code-a-long

1. Open up BigQuery in the [Google Cloud Console](https://console.cloud.google.com/bigquery). If you don't already have a Google Cloud account, it is easy to create one. Also, everything we'll do in this demo only processes X GB of data, so the resources we'll consume are well within [Google Cloud's free tier](https://cloud.google.com/free).

2. As mentioned in the introduction, BigQuery houses public datasets that included forecasts from weather models as well as weather observations we can use to improve on future forecasts. Let's first add the weather model output to our project. Select **+ ADD DATA --> Explore public datasets**. The weather model output we'll use is NOAA's _Global Forecast System_, or GFS.