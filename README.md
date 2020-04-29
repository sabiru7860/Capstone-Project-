#Intro
The financial markets are a great way to make money. There are two types of people who make up the financial markets. One is the investor, and another is the trader. An investor is someone like Warren Buffet, they buy and hold for years. On the other hand, a trader is someone who buys and sells in a short time period. The time period depends on the type of trader you are. One type of trading that is popular is day trading. Day trading is when you buy a security and sell it in the day. People love this strategy because they aren’t in the markets for too long. The problem is due to federal laws, to day trade you need $25,000  in your account. Many people don’t have that type of money to put aside to day trade. With my project I am going to find a way around this. I am going to create a trading strategy. The trading strategy is to buy right before the market closes and sell right after the market opens. This way you will not be in the market for too long. I am also going to create time series models for all stocks in the Nasdaq that predicts one day out with high confidence. This way people can know what stocks to buy. I will be using the stocks from the nasdaq 100. The nasdaq 100 contain the biggest 100 non financial companies. I chose them because they are relaiable and wont go bankrupt the next day.

# EDA
I used a python library called yfinance to get all my stock data. After i got my stock data the first idea i had was to split my stock based on thier volitlilty. This helped me split up my stocks within each other. What i also did was i decided that i wanted decide to see the correlation within the stocks with each groups. 
Lastly i decided to run a seasonal decompose of my all my stock correlation groups. I saw how all of my stocks have a slight seasonalality

#Baseline model
For my baseline model i used a very a simple model that predicted the mean for every time step. I calculated the rmse for each stock using this method. My main goal is to improve on these numbers


# Sarimax model
I decided to use the SARIMAX model statsmodel has. I also used a walk foreword method along with my sarimax model so i would have better accuracy with my sarimax model