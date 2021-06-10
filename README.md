# Stock-Market-Analysis-and-Prediction

## Predicting market prices using exogenous variables

# Scenario:

## As an analyst for an investment firm I am tasked with finding variables, or indicators to more accurately predict market movements and maximize returns.

# Data:

S&P 500 monthly prices along with 10 other economic and financial variables grabbed from https://www.multpl.com/s-p-500-historical-prices.

<img src="https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/init_data.png" width="400" height="600">


## EDA

I started by collecting the data from multpl using 'read_html.' See the full process in the data_gathering file.
Once I had the data I inspected it for trends and found a clear upward trend with time for most of the data
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/data_graph.png

Given this I ran a correlation table.
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/corr_table.png
Much of the data was somewhat correlated but Earnings, Dividend, Inlation, and CPI had the strongest connections.

Given this upward trend I ran a stationarity test and found that all but a few variables not stationary.
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/stationarity.png
Even after 50 lags stationarity was not met.

## Initial models

I started by running a baseline ARIMA model with no exogenous variables and using itertools to find the best pdqs.
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/initial%20model.png
This created an inital model with an AIC of 7034.6674 and a test RMSE of 311.0111.

Next I ran the same model but with each of the variables.
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/init_sarimax_table.png
All of these models underperformed the baseline. 10 year treasury rate and dividend did, however, stand out doing well by camparison.

Using the top variables I ran a SARIMAX model for each combination.

(top 5 models by test RMSE)
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/combo_exog_tables_RMSE.png

(top 5 models by AIC)
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/combo_exog_tables_aic.png

This time many of the models did better than the baseline with the 10 year treasury rate, dividend, and earnings doing the best.
Most notably the SARIMAX model with 10 year treasury rate, and tuning of pdqs did better than the more complex models with the 2nd best test RMSE and 4th best AIC. It also was statisticly significant in this and other top models.
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/treasury_rate_grph.png
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/treasury_rate_table.png

## Facebook Prophet Models
Next, I ran the same variables through facebook prohpet modesl.
I created a baseline with just price and with each variable.
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/fb_pro_table.png
This time most of the variables did noticeably better than the baseline. 
Agaain I ran combinations of all of the top models through this process.
https://github.com/s-shader/Stock-Market-Analysis-and-Prediction/blob/main/pics/fb_pro_tables2.png
This further shrunk the errors, however, while it was much better than the baseline it was worse than the ARIMA and SARIMAX models.
It did however, highlight 10 year treasury rates and inflation as having the most significant impost.

# Conslusion 
My best models failed to predict future prices to a degree of accuracy that would be usefull. They did, however, show the importance of certiane variables when looking at market prices.
10 year treasury rates consistently improved model accuracy and was statisticly significant. Moreover, it at a fairly consistent coefficient ranging from -2.7 to -3.1. Earnings, inflation, and CPI were also quite usefull interms of increasing model accuracy. 

Finnaly, this process did successfully serve as a "proof oof concept" for using market and economic variables to predict future prices. While these models were not very accurate, they did imppove relative accuracy by as much as 33.1%. This would, at least, imply that with the right combination of variables in the right model accuracy could be improved enouigh to be usefull.

# Future Work
As noted above my ARIMA models were much more accurate than the facebook prophet models. As such, experimenting with other types of models could prove profitable. Additionaly, my models only used 10 exogenous variables. It is probably worth exploring other financial and economic variables.

Finnaly, my model was over a long time span from 1872-2020 and on a monthly basis. It is quite possible that there are trends that exist on a shorter timespan or on an intra-monthly basis.

