# The Market for Roman Coins on eBay 
## Understanding Market Dynamics and Predicting Price

My goal for this project was to understand the dynamics of the market for Roman coins. Using the thriving market for ancient coins on eBay as a proxy, I utilized eBay's API to scrape, build, clean, and mine a dataset of more than 18,400 Roman coin sales over 6 weeks. Using available features (like: bidcount, watchcount, auction type, etc.) and a variety of additional features I extracted from textual descriptions (like: Emperor name, coin metal, and quality), in the end, I was able to model 84% of the variation in coin price using a random forest regressor and automated a script to regularly check eBay and alert me by email of potential bargains.

### The Market
On an average week (in Mar. & Feb. 2018), *1882* new listings valued at *$109,000* are posted by sellers and *3859* bids are made by buyers. Of course, with more than 71 emperors (the exact number depends on how you interpret the 395 AD East/West schism) minting a variety of coin qualities (silver/gold, clean/unrecognizable, etc.) and in a wide range of quantities, individual coins can differ greatly in price and scarcity. 

Unlike today, when we tend to place long dead rulers on our coins, in ancient Rome emperors typically minted coins of their own likeness. Below, each bubble represents coins minted by a particular emperor, each bubble's size is a proportional representation of the mean price (bigger = more expensive), and each bubble's color represents scarcity (redder = rarer). Unsurprisingly, note the diversity of sizes(*prices*), price varies widely by emperor.   

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/bubbles.png" height="550" width="680">
</p>

As you can see from the clustering of large red bubbles in the center, there is clearly a positive correlation between scarcity and price (i.e. as a coin becomes scarcer, it increases in value). On the other hand, certain emperors' coins seem to fetch higher prices despite being relatively prevalent. Once again, you can see this clearly below. This graph shows coins by emperor with *bids per auction* (a demand proxy) on the y-axis and the *log of mean price* on the x-axis (again, the redder the circle, the rarer the coin):

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/marcusBackground.png" height="550" width="680">
</p>

The graph above shows that increased consumer demand (bidding) drives prices up and that rarer coins tend to be have higher prices regardless of bidding. However, this is only a tendency, not a rule. The slope of the trend line and dispersion of scarcity make clear that there are other factors at play. 

### Dominant Player

Markets for boutique goods (paintings being one prime example) are particularly ripe for manipulation and pricing guides can be unreliable. In that light, I was interested in how formalized the market for Roman coins was- i.e. are the sellers mostly amateurs or mostly professionals? Grouping the data by zip code (see below) revealed that nearly 48% of sales were originating in Queens, NY. This signaled to me that a handful, or possibly just one professional player has captured an enormous market share (the larger the red bubble the more sellers in that zip code, states are shaded according to their population).

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/USmap.png" height="400" width="550">
</p>

In fact, coins being sold from Queens are on average 54% more expensive than those from the rest of the country. This discontinuity may be signalling that buyers are willing to pay an authenticity premium (professional assurance that the coins are not replicas), that the coins are of higher quality, more effectively marketed, or that they have monopolized a particular supply-chain (one also can't rule out a more nefarious alternative). 

Let's take a look now at the distribution of price across *all* coins. 

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/histprices.png" height="420" width="800">
</p>

First, given that this is scaled logarithmically, we can see that an unscaled distribution would have a long right tail (i.e. more lower price coins and fewer higher priced coins). Second, it is likely that the Queens seller has a certain segment of the market cornered and is likely methodical in price-setting (the dark blue bins are clustered). Third, there are several outliers that will have to be accounted for or dropped before analysis. 

### Submarkets

Another area of variance is in listing type. Not everything on eBay is an auction, in fact, most sales (70% of them) are not auctions. Why does this matter? Because the average price, by listing type, varies from $39 for an auction (30% of all listing types) to $207 for store inventory (60% of all listing types). As you can see in the graph below, the vast majority of high price coins are coming from professional sellers that may be able to largely determine price points (dependent, of course, on market elasticity). If you're curious, 52% of the 11,485 store inventory listings originate in Queens. 

(*AuctionWithBIN* indicates that you can either bid or 'buy it now')
<p align="right">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/legend.png" height="120" width="120">
</p>
<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/newnewlisting.png" height="400" width="550">
</p>

### The Model and Feature Importance

The final model includes 74 features ranging from continuous demand factors (watch count, bid count) to dummy variables for product characteristics (ex. metal type and emperor). On training data, the model accounts for ~74% of the variation in price (versus 84% on the full dataset- where overfitting is a significant limitation). Before arriving at a random forest regressor for my final model I tested a variety of alternative models, including neural network, OLS, and boosting. Likewise, more than 20 insignificant features were exlcuded from the final model and I ruled out a bag-of-words model using the item description. 

The following features in the final model are the most influential in capturing price variation: 

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/feature_importance.png" height="310" width="550">
</p>

Interestingly, 'best offer enabled' tops the list. This is a listing characteristic that allows a prospective buyer to make an offer below the listed price. Also, in the top ten features are the 'Queens seller' dummy variable, whether the coin is silver, and the two demand proxies: bid count and watch count. 

### Limitations and Moving Forward

Several factors, some inherent to the market and others part of the data collection process, present issues for external validity. First, even after restricting observations to a range of $3-$1000, the model is less successful in predicting prices on the margins- with efforts to increase feature complexity unsuccessful in reducing these errors. Second, feature creation is reliant upon the seller listing relevant characteristics in the title (there are no mandatory fields in eBay for coin metal, emperor, etc.). If certain sellers are systematically including or excluding this information, a real possibility, predictions will be biased. 

The model can also be manipulated by a seller that doesn't include the real quality of the coin in their description. Moving forward, I can mitigate this problem by incorporating coin images into the model by training a convolutional neural network
to classify coin quality. 
