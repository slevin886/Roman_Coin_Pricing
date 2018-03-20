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
