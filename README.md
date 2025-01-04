# Gold Prediction Project

## Project Overview
During times of economic uncertainty and turmoil, owning gold is often looked at as a place of security for investors. The reason being is gold serves as a strategic asset in financial portfolio diversification due to its low correlation to other assets such as stocks or bonds. One of the major importances of gold is its stability, which is caused by its resilience to inflation. Over the course of the last 10 - 20 years, we have seen a fluctuation in the price of gold, characterized by periods of growth and decline. This price fluctuation has been indicative of the respective year’s economic growth. The mirroring of economic conditions as well as protection from inflation is a major driver for gold’s significance.

The question that I sought to answer and discover is what the price of gold would be in the next few years, given past historical data. I wanted to determine if I could predict the price of gold on January 1, 2026, through the use of quantitative data consolidated daily over the last twenty years. The machine learning technique I decided to use to answer this question was time series analysis. I wanted to see if the data’s trends, seasonality, and cyclical nature would help me formulate a numerical prediction for the next year’s gold price. With this prediction, perhaps it could give us insight into how the economy is slated to perform.

## Repository
The repository for my project can be found at 
+ https://github.com/RayyanWaseem1/Gold-Predictor/blob/main/GoldPredictionProject.ipynb

## Dataset
The dataset that was used in this project was sourced from Kaggle. The modality of the data was largely time series temporal data consisting of multiple features (columns) including the date, the time, the opening price, the highest price during the day, the lowest price during the day, the closing price, and the total volume of gold traded on that particular day. This was again consolidated daily from 2004 to 2024. The sample size for the daily interval dataset was 5205 data points. This data is deemed very important as it gives us a wide scope of all the different aspects that go into gold pricing. We get to see the many fluctuations of pricing from an outsider point of view, which gives us the ability to make more accurate predictions.

+ https://www.kaggle.com/datasets/novandraanugrah/xauusd-gold-price-historical-data-2004-2024/data?select=XAU_1d_data_2004_to_2024-09-20.csv

## Machine Learning Methodology
The methodology used for this project was a time series analysis, spanning over 20 years. The context in which this project was conducted was to cater to the finance/business industry. The reason that I chose a time series analysis over other methodologies was due to the nature of the data, which consisted of observations with a temporal ordering. The way time series analysis works is that it analyzes a temporal sequence of data points, at constant time intervals, in order to identify trends, patterns, and seasonal variations. This allows for the forecasting of future values based on historical data and past observations.

While using time series analysis, I did not need to split my data into training, testing, or cross-validation splits, as I am taking into account all of the variables in order to predict one target variable, the daily closing price. Also randomly sampling and splitting up the data would ruin the temporal ordering of the data thus not allowing us to predict the price of gold based on previous observations.

I did not need to preprocess any data. My dataset was sourced from Kaggle and already was distributed as preprocessed and clean. There were no missing data points, and the data was balanced. As a result, I was able to immediately get to work using the dataset.

The main libraries used were NumPy, Pandas, Matplotlib, Seaborn, Plotly, and Statsmodels. As well as this, I imported PMDARIMA in order to derive the SARIMAX.

## Results
Initially, I plotted the price of gold from 2004 up until 2024 to get a general understanding and visualization of how the price of gold has changed over the course of the last twenty years.

<img width="652" alt="Screenshot 2025-01-04 at 3 31 34 PM" src="https://github.com/user-attachments/assets/6b342e92-8959-45e2-addc-35c965cea1c1" />

After plotting the general trend in price, I conducted an STL Decomposition to visualize the trends, seasonality, and residuality of the daily closing price. After the STL Decomposition, I found it important to run an Augmented Dickey Fuller test on my time series data. The reason for this test being implemented is to determine if the data is actually stationary. Stationarity is an important concept in regard to time series, because it allows us to determine if the probability distribution changes with time. If the distribution does in fact change with time, then the data cannot be deemed stationary.

<img width="505" alt="Screenshot 2025-01-04 at 3 31 52 PM" src="https://github.com/user-attachments/assets/860912ff-337c-468c-a074-5a64946f4f8c" />

<img width="652" alt="Screenshot 2025-01-04 at 3 32 06 PM" src="https://github.com/user-attachments/assets/d138bc33-8793-4904-ac7a-63662650a288" />

After conducting the initial Augmented Dickey Fuller test, my data was deemed non stationary, with an incredibly high p-value. The method I used to resolve this was to difference the data across a period of twelve months, in order to make it stationary. After differencing the data, the p-value was then shown to be low enough, making the stationarity statistically significant. Because I differenced the data, I then applied a Box-Cox transformation to inverse this and return with the unnormalized original data.

Once this was completed, I conducted a SARIMAX grid search, which incorporates a seasonal adjustment into my data, in order to determine the best AIC score. AIC stands for Akaike Information Criterion, and seeks to reward the accuracy of my prediction and penalize its complexity. So finding the best AIC score represents how accurate the time series has been in its predictive nature.

Finally, I decided I wanted to predict the daily closing price, as compared to other metrics such as the opening price or the highest daily price. The reason for choosing the closing price is because it represents the final consensus of the gold’s value at the end of each trading day. Essentially, it acts as a benchmark to compare price movement over time and gauge the market sentiment of gold. In order to make my prediction, I incorporated the data starting from 01/01/2004, and I wanted to predict the price action up until 01/01/2026. As my project will be completed near the end of 2024 and towards the beginning of 2025, I wanted to see the movement of gold for the upcoming year. After plotting out the forecasted results onto a graph, you can see that the price of gold would be predicted to be around $4,000 per ounce around 01/01/2026

<img width="652" alt="Screenshot 2025-01-04 at 3 32 21 PM" src="https://github.com/user-attachments/assets/f7ea4b66-3ee7-4af7-b98c-468f0af13cec" />

## Lessons Learned
Throughout the duration of this project, I learned quite a lot in terms of price prediction and time series analysis. When my project was first conceived and introduced, I had a lack of understanding regarding time series data and assumed I could predict the price of gold using multiple linear regressions. While this could have been used to crudely determine the price, it would have been inaccurate and would not have incorporated seasonality, trends, or residual factors into the price prediction. The model also would have had somewhat of a high bias, as it would be fitting the past historical data onto a straight line. As I progressed throughout my education and learning, I started to learn more about this type of analysis and understand how beneficial it could be to implement as opposed to linear regression

While working on this problem, I realized that conducting the Augmented Dickey Fuller test not adjusted for stationarity was not enough to help me determine an accurate prediciton. It was important to implement the transformation to get the normalized values and difference the data such that it is stationary. This allowed for higher accuracy. As well as this, I spent a lot of time on the SARIMAX grid search. I tampered with perhaps using a standard ARMA or ARIMA, but concluded that using SARIMAX would lead to more accurate results due to its incorporation of seasonality.

Most of the challenges that I faced were trying to determine how my project would be beneficial to those in the financial industry. I went back and forth between choosing the opening price, closing price, and highest/lowest price that day. As I was doing research on other similar projects, I came to the conclusion that the daily closing price would be the best value to forecast.

To those reading and reviewing my first project, I hope to have provided a solid foundational understanding on time series analysis and how it could be used in price prediction of not only gold, but other assets as well, such as stocks and bonds. This machine learning methodology is incredibly useful when it comes to determine what our economic outlook could look like in the upcoming years.
