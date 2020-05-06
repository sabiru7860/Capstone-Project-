
#Intro
The financial markets are a great way to make money. There are two types of people who make up the financial markets. One is the investor, and another is the trader. An investor is someone like Warren Buffet, they buy and hold for years. On the other hand, a trader is someone who buys and sells in a short time period. The time period depends on the type of trader you are. One type of trading that is popular is day trading. Day trading is when you buy a security and sell it in the day. People love this strategy because they aren’t in the markets for too long. The problem is due to federal laws, to day trade you need $25,000 in your account. Many people don’t have that type of money to put aside to day trade. With my project I am going to find a way around this. I am going to create a trading strategy. The trading strategy is to buy right before the market closes and sell right after the market opens. This way you will not be in the market for too long. I am also going to create time series models for all stocks in the Nasdaq that predicts one day out with high confidence. This way people can know what stocks to buy. I will be using the stocks from the Nasdaq 100. The Nasdaq 100 contain the biggest 100 nonfinancial companies. I chose them because they are reliable and won’t go bankrupt the next day.









# Navigation
PowerPoint which I used to present this project is in Capstone.pdf 

The environment while creating this project is under envirement.yml. This file can be used to create the environment to run the book.

The entire project was done on one notebook. The book name is Capstone Project.ipynb

In order to re-create analysis each cell can be done sequentially 



# Citations
Some code used in this project came from the internet. Here are the links

[Function to Grid search SARIMA model] (https://machinelearningmastery.com/how-to-grid-search-sarima-model-hyperparameters-for-time-series-forecast)

[Forward Step SARIMA model] (https://www.liip.ch/en/blog/time-series-prediction-a-short-comparison-of-best-practices)
# Importing Data and Tools
For the first part of my project i needed to import all of my tools and data. For all the tools I used you can look at the first cell of my notebook. Next I used a python library called yfinance [yfinance](https://pypi.org/project/yfinance/) to get all my stock data. The stocks i decided to use were all the stocks in the NASDAQ 100. These stocks are the biggest 100 nonfinancial companies in America. So, the chances that these stocks bankrupt the next day is impossible. They are safe companies to trade with. 

#Data Cleaning
For data cleaning I wanted to make sure my data fits my needs that is required for my process. After looking at my data I had a great understanding of what i needed to do to clean my data steps.
## What needs to be done?
1. Drop Columns everything except opening price 
2. Drop potential Stocks (If for whatever reason stocks didnt download correctly or have missing data)
3. Delete next day holding rows from dataset
4. Fix Shape of my dataset
5. Normalize data

You can learn more about my process in the data cleaning section of my Capstone notebook

#Initial EDA
 Explanatory Data Analysis is the process where you explore your data. You do this step so you can become more familiar with your data. For my eda I decided to look at two interesting features that all stocks have
 
 1. Volatility 
 2. Correlation

#Volatility
Volatility is a financial term for standard deviation. It basically shows you how a stock behaves. If a stock has a high standard deviation then it is prone to have wild swings. These stocks are best for people who love risk. On the other hand stocks that have low volatility are stocks that don’t move too much, These are better for people who have low risk tolerance. i split my dataset into 3 groups. I calculated standard deviation for the opening price of each stock. Then sorted list based on the size of standard deviation. Finally i used that to bucket my stocks as follows:

1. Low 
  1. The 50 stocks with lowest std
2. Medium
	1. Stocks with the 51st to 26th highest std
3. High
	1. Top 25 stocks with the highest std

You can find more about this process under the Volatility head in my Capstone notebook Capstone Project.ipynb


#Correlation
Correlations between stocks prices appear frequently in the markets. One general rule in investing is to have a diversified portfolio. In other words, we do not want stocks that have strong correlation with each other. 
So, what I did was within each volatility group i decided to see if stocks correlate with other stocks within them. I decided to use a correlation of 50% or more. This is something i am going to refer as a positive correlation. 

Another way correlation will help me is that i decided that if a stock has a positive correlation to lots of other stocks, I will model that stock and apply it to the stocks it has a positive correlation with. This will save time and computing power.

## Steps i am going to achieve this
In each volatility group I am going to:
1. use the correlation function to see the correlations among the stocks.
2.From those results I am going to select the stock that has the greatest number of positive correlations within that group.
3. Tune model for that single stock so that I can apply it the other stocks it is positively correlated with.
4. For all the stocks that did not have a positive correlation with that given stock i am going to tune a model for those stocks individually.


### Example
Capstone Project.ipynb
For a quick example of this check out my capstone notebook. Under Correlations within low volatility group, I showed all the steps with in depth for the low volatility group

#Process for tuning the model

Now it is time for the modeling process. Like i mentioned before we found stocks that correlate with others in that group the most. After i found the stock it was time to model it. The steps I am going to take is as follows

## Steps
1. Get stock that has the strongest correlations within the volatility group
2. Decompose it
3. Find Baseline model
4. Use grid search to tune my model
5. Apply the tuned model to the stocks it had a positive correlation with.
6. Whatever stock did not have a positive correlation with that specific stock i am going to repeat the process to tune a model for it.

Here is a example what this process looks like for the low volatility group.

# Modeling for Low Volatility Group
When it came to my low Volatility group the stock that had the most correlations of 50% or greater within that group is the stock VRSN. VRSN has 36 positive correlations within the low volatility group. This is the stock we are going to model. After that we are going to apply the same model to the stocks it correlates positively with. 


## Steps
1. The first step is to decompose the trend of VRSN. I am using Stats models to decompose my stocks (Picutre of Decompose) After decomposing it we realize multiple things. First, we understand the general trend is rising. We also realize there is slight seasonality. I am assuming this is  most likely because of earnings and other company related news. I am assuming this......

2. Next step is to create a baseline model using package stats models. The modeling process uses a SARIMA model (although i imported a SARIMAX model because i found the implementation of the model easier to work with). Here is a picture of stock VRSN with the prediction and the rmse. (Picture of VRSN and the RMSE)

3. Tune model using Grid Search
i tuned my model using a grid search function i found online Function to [Grid search SARIMA model] (https://machinelearningmastery.com/how-to-grid-search-sarima-model-hyperparameters-for-time-series-forecast)(all citations will be linked to the beginning of the README)

here is a graph the same VRSN stock and prediction along with the rmse score using the tuned model.(picture)

4. Apply the tuned model (in other words apply the SARIMA model with the same hyper params as the tuned VRSN model) to all of the stocks that it has a positive correlation with. 

Example of stock that has highest positive correlation and stock with lowest positive correlation. (for each do the same process as others)

5. Lastly i am going model each of the stocks it did not have a positive correlation with.

For example  here is the stock ROST. Below is a graph of the baseline SARIMA model applied to its time series as well as the rmse.(picture)

Here is the graph of the tuned VRSN model applied to ROST and its rmse.(picture)

Here is a model that is tuned to just on ROST and its rmse.(pic)

As you can see......

Of the low volatility group that didn’t have a positive correlation with VRSN, i was only able to tune 4/16 of them.

Now to use this strategy you want to compare the stocks recent closing price to the predicted opening price of tommaorw.

#Future Work
For the time being this is as far as I was able to make it on the project. The main reason why is because the grid search has a computation time of around 90 minutes for each model on the hardware, I had access too. For my future work I really want to continue on creating predictions for my middle and high volatility groups. Another thing I want to focus on is trying to model and predict volatility using the GARCH model. Lastly, I want to find out is there any alternative way to help find a lower RMSE. For example, I am going to try out using an LSTM neural network to model my stocks. Maybe that might lower my RMSE because it uses neural networks to make predictions.
