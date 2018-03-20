# The Market for Roman Coins on eBay 
## Understanding Market Dynamics and Predicting Price

While on a roadtrip in Spain, I chanced into a collection of recently unearthed coins in (of all places) a local gas station on a desolate highway in Andalusia. Learning from the farmer selling them that they were monedas romanas (Roman coins), I gladly paid the 20 euros he was asking and was off. For nearly 2000 year old coins, it felt like a steal. But was it?

My goal for this project was to understand the dynamics of the market for Roman coins. Using the thriving Roman coin market on eBay as a proxy, I used eBay's API to scrape completed and active sales and built a dataset of more than 18,400 Roman coin sales over 6 weeks. Using available features (like: bidcount, watchcount, auction type, etc.) and a variety of additional features I extracted from textual descriptions (like: Emperor name, coin metal, and quality), I was able to model 84% of the variation in coin price using a random forest regressor. 

### The Market
On an average week (in Mar. & Feb. 2018), 1882 *new* listings valued at *$109,000* are posted by sellers and *3859* bids are made by buyers. Of course, with more than 71 emperors (the exact number depends on how you interpret the 395 AD East/West schism) minting a variety of coin qualities (silver, gold, copper- among other features) and amounts, individual coins can vary widely in price and scarcity. 

Below, each bubble represents an individual emperor, each bubble's size is a proportional representation of the mean price (bigger = more expensive), and each bubble's color represents scarcity (redder = rarer). 

<p align="center">
  <img src="https://github.com/slevin886/Roman_Coin_Pricing/blob/master/images/bubbles.png" height="550" width="680">
</p>
