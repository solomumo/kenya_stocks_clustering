# Project Brief: Kenyan Stock Data Scraping & Clustering Algorithm

# Big Picture
Scrape daily Kenyan stock price data over 10 years and build clusters of the individual stocks based on daily returns (%) and standard deviation. Include visualization of the clusters with individual stocks as bubbles with ticker symbols included.

# Motivation
1.	Create datasets using Kenyan data for further exploration by myself and other data aficionados. 
2.	Diversification is investment and portfolio management 101! The output of this work leverages big data (almost ¼ million data points) to understand returns and volatility differences in listed stocks. For diversification’s sake, an investor would prudently pick stocks from different clusters to minimize portfolio risk. 

# Data Needs
1.	Ticker symbols (key) and relevant sector (value) in a dictionary
2.	Closing and opening prices – to compute returns and perform log transformation 

# Data Collection
1.	Create for-loop with time delta object per day – e.g., 365*3 for 3 years or 365*10 for 10 years (for x in range delta.days)
2.	F-string containing base URL and a variable ‘date’ that starts as a constant and adds the delta.days object at each iteration
3.	Use Pandas read_html method to access site with raw data
4.	Append relevant data (already in form of a Pandas DataFrame) in a mega list at each iteration outside the loop
5.	Concatenate all DataFrames in the mega list into one DataFrame and save raw data in CSV (should be almost 250,000 records).

# Data Preparation
1.	Read saved file into a DataFrame (DF)
2.	Create a copy of the DF with only relevant features – price and previous
3.	Replace non-numeric data into numeric by replacing commas with nothing and converting DF into the float datatype
4.	Create new feature ‘Returns’ – divide current price by previous price – and perform logarithmic transformation of the new feature. 
5.	Group all returns using the ticker symbol – i.e., find mean and std of returns per ticker. 
6.	Create a DF with the grouped mean returns and std dev of returns. 

# Modelling
1.	Plot mean returns against std dev using a simple scatterplot (use pyplot or seaborn) – include ticker symbols next to the relevant point
2.	Compute the z-scores to remove outliers from data – clustering is sensitive to outliers. Outliers have a z-score of less than -3 or greater than 3. 
3.	Create an elbow curve to guide the number of clusters to build. Value of K is at the elbow point
4.	Initialize and fit K-Means model to the DF (input) containing mean and std dev of returns 
5.	Predict the inputs and plot the clusters (use seaborn here)
6.	Save the predictions into a DF that includes the ticker symbol, the sector, and cluster. 
