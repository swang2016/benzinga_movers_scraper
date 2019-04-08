# Overview #

This project scrapes headlines of stock price movements from various Benzinga's Movers article series (https://www.benzinga.com/movers). The scraper functions pull headlines from the following time periods and article series:

* 10/12/2015 - 06/06/2016: Mid-Afternoon Market Update 
  * (Example: https://www.benzinga.com/news/earnings/16/02/6222002/mid-afternoon-market-update-nasdaq-down-over-3-ttm-technologies-shares-g)
  
* 06/06/2016 - 10/16/2017: Mid-Day Gainers/Losers 
  * (Example: https://www.benzinga.com/news/17/06/9596357/15-biggest-mid-day-gainers-for-monday)
  
* 10/16/2017 - Present: Biggest Movers From Yesterday 
  * (Example: https://www.benzinga.com/news/19/04/13491633/52-biggest-movers-from-yesterday)
 
In addition to scraping headlines, additional functions for obtaining historical price and volume data using the IEX API are included.

Lastly, functions for scraping earnings filing dates from Marketwatch are also available.

# Usage Examples #
Examples of how to use the functions mentioned above are also shown in the Jupyter notebook, `benzinga_scrape.ipynb`, in the Scripts folder.

## Scraping Headlines ##
Initial data pull (only goes back to 10/12/2015, can choose to specify more recent dates):

`df = get_initial_biggest_movers_data('October 12, 2015')`


If you already have headlines saved and only want to update the data with more recent headlines:

`new_dat = get_new_benzinga_data(old_dat)`

Where `old_dat` is a dataframe of headlines already saved. `new_dat` will be new headlines retrieved from dates after the most recent headline in `old_dat`.

## Getting Price and Volume Data ##
Initial data pull (specify how far back you want to go, IEX API only goes back 5 years):

`prices, volumes = get_initial_price_data(tcks, '2015-10-01')`

where `tcks` is a list of tickers.

If you already have price and volume data saved and only want to update with more recent data:

`new_prices, new_volumes = get_new_price_data(tcks, prices)`

where `tcks` is a list of tickers and `prices` is a dataframe of already saved prices. `new_prices` and `new_volumes` will have the latest prices and volumes updated for tickers already saved as well as entire price and volume history going back 5 years for tickers not already saved. 

## Getting Earnings Reports Dates ##
Initial data pull (specify how far back you want to go):

`earnings = get_earnings_dates(tcks, '2015-10-12')`

where `tcks` is a list of tickers.

If you already have dates saved and only want to update with more recent data (once again, specify how far back you want to go):

`new_earnings = get_new_earnings_dates(tcks, earnings, '2015-10-12')`

where `tcks` is a list of tickers and `earnings` is a dataframe of earnings dates already saved. `new_earnings` will have the latest earnings dates updated for tickers already saved as well as the entire earnings date history going back to the specified date for tickers not already saved.

Note: Marketwatch does not have filing dates for some stocks that are no longer traded/companies that were acquired/etc.

## Scraped Data ##
The Scripts folder contains a Jupyter notebook, `benzinga_clean.ipynb`, that shows how the headline, price, volume, and earnings dates data might be cleaned and combined. 

In the Data folder you can also find pre-scraped data from 10/12/2015 - 04/04/2019 using the functions mentioned above. The pre-scraped data includes:

* `stock_headlines.csv`: CSV of headlines, associated tickers, and dates 
* `stock_prices.csv`: CSV of tickers and their prices for the date range of 10/12/2015 - 04/04/2019
* `stock_volumes.csv`: CSV of tickers and their volumes for the date range of 10/12/2015 - 04/04/2019
* `filing_dates.csv`: CSV of tickers and their earnings filing dates for the date range of 10/12/2015 - 04/04/2019
* `stock_headlines_cleaned.csv`: `stock_headlines.csv` with additional features generated from `stock_prices.csv` and `stock_volumes.csv`. Example code showing how this file was made is in `benzinga_clean.ipynb` in the Scripts folder.

# Analysis #
A sampling of some exploratory analysis done on this data can be found in `benzinga_analysis.ipynb`, in the Scripts folder. A forthcoming Medium post will be based on this analysis. 
