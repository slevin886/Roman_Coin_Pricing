# The Market for Roman Coins on eBay 
## Understanding Market Dynamics and Predicting Price

A few years back, I was on a road trip in Spain and came across a small collection of dusty old coins on. Learning from the young woman selling them that they were *monedas romanas* (Roman coins), I was intrigued and happily paid the 20 euros she was asking. Tweny Euros for nearly 2000 year old coins?! I couldn't believe my luck, it felt like a steal. But was it?

My goal for this project was to understand the dynamics of the market for Roman coins. Using the thriving market for ancient coins on eBay as a proxy, I utilized eBay's API to scrape, build, clean, and mine a dataset of more than 18,400 Roman coin sales over 6 weeks. Using available features (like: bidcount, watchcount, auction type, etc.) and a variety of additional features I extracted from textual descriptions (like: Emperor name, coin metal, and quality), in the end, I was able to model 84% of the variation in coin price using a random forest regressor and automated a script to regularly check eBay and alert me by email of potential bargains.

### The Market
On an average week (in Mar. & Feb. 2018), 1882 *new* listings valued at *$109,000* are posted by sellers and *3859* bids are made by buyers. Of course, with more than 71 emperors (the exact number depends on how you interpret the 395 AD East/West schism) minting a variety of coin qualities (silver/gold, clean/unrecognizable, etc.) and in a wide range of quantities, individual coins can differ greatly in price and scarcity. 

Below, each bubble represents coins minted by a particular emperor, each bubble's size is a proportional representation of the mean price (bigger = more expensive), and each bubble's color represents scarcity (redder = rarer). 

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/bubbles.png" height="550" width="680">
</p>

As you can see from the clustering of large red bubbles in the center, there is clearly a positive correlation between scarcity and price (i.e. as a coin becomes more scarce, it increases in value). On the other hand, certain emperors' coins seem to fetch higher prices despite being relatively prevalent. Once again, you can see this clearly below. This graph shows coins by emperor with *bids per auction* (a demand proxy) on the y-axis and the *log of mean price* on the x-axis (again, the redder the circle, the rarer the coin):

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/marcusBackground.png" height="550" width="680">
</p>

The graph above shows that increased consumer demand (bidding) drives prices up and that rarer coins tend to be have higher prices regardless of bidding. However, this is only a tendency, not a rule. The slope of the trend line and dispersion of scarcity make clear that there are other factors at play. 

Markets for boutique goods (paintings being one prime example) are particularly ripe for manipulation and pricing guides can be unreliable. In that light, I was  interested in how formalized the market for Roman coins was- i.e. are the sellers mostly amateurs or mostly professionals? Grouping the data by zip code (see below) revealed that nearly 48% of sales were originating in Queens, NY. This signaled to me that a handful, or possibly just one professional player has captured an enormous market share (the larger the red bubble the more sellers in that zip code, states are shaded according to their population).

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/USmap.png" height="400" width="550">
</p>

In fact, coins being sold from this zip code are on average 54% more expensive than other coins. This may be signalling a authenticity premium (professional assurance that the coins are not replicas), overall higher quality, and/or superior marketing and price-setting. In the histogram of current coin prices below, several things come in to view.

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/histprices.png" height="420" width="800">
</p>

First, given that this is scaled logarithmically, we can see that an unscaled distribution would have a long right tail (i.e. more lower price coins and fewer higher priced coins). Second, it is likely that the Queens seller has a certain segment of the market cornered and is likely methodical in price-setting(the dark blue bins are clustered). Third, there are several outliers that will have to be accounted for or dropped before analysis. 
