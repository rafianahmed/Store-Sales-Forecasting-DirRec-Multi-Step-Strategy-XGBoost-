Store Sales Forecasting – DirRec Multi-Step Strategy (XGBoost)
This repository implements a 16-step ahead forecasting model for the Kaggle Store Sales – Time Series Forecasting competition using the DirRec (Direct-Recursive) strategy and XGBoost.

Project Overview
The goal of the competition is to predict daily sales for 16 future days across multiple time series defined by:
Stores (store_nbr)
Product families (family)
This repository builds a forecasting solution that:

✔ Uses 4 historical lag features
✔ Produces a 16-step forecast with 1-day lead time
✔ Trains one model per forecast horizon step (DirRec strategy)
✔ Works for all store/family combinations simultaneously
✔ Runs efficiently with XGBoost

 Forecasting Task Definition
Component	Value
Forecast origin	2017-08-15
Forecast horizon	2017-08-16 → 2017-08-31
Forecast length	16 steps
Lead time	1 day
Lag features used	4 days (lag 1-4)

Strategy
DirRec (Direct-Recursive)
 Forecasting Strategy
The DirRec strategy combines the benefits of both Direct and Recursive forecasting:

✔ Direct
One model per forecast step → better accuracy
✔ Recursive
Uses predicted values as new inputs → captures sequential dependency

➤ DirRec

y₁ is predicted first

That prediction becomes a new lag value

Then y₂ is predicted using an updated feature window

Repeated until y₁₆

This reduces error propagation compared to recursive, while allowing dependency learning unlike pure direct.

 Model Pipeline

1️⃣ Load and sort time series
2️⃣ Create 16 future target columns: y_1 … y_16
3️⃣ Create 4 lag features: lag_1 … lag_4
4️⃣ Drop missing values
5️⃣ Train 16 XGBoost models, one per forecast step
6️⃣ Predict sequentially, updating input features after every step
7️⃣ Return a 16-day forecast dataframe


Tech Stack
Python, Scikit-Learn, Pandas, NumPy, Matplotlib, Seaborn, XGBoost, LightGBM, TensorFlow/Keras (LSTM), Git, Jupyter, PyTorch

⚠️ Download dataset manually from Kaggle into the project root.
https://www.kaggle.com/competitions/store-sales-time-series-forecasting/data?select=train.csv 


