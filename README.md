# **TvDatafeed**

A simple TradingView historical Data Downloader

If you found the content useful and want to support my work, you can buy me a coffee!
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/StreamAlpha)

## Installation

This module is installed via pip:

```
pip install --upgrade --no-cache-dir git+https://github.com/nanpuhaha/tvdatafeed.git
```

For usage instructions watch these videos-

v1.1 tutorial with installation and backtrader usage

[![Watch the video](https://img.youtube.com/vi/f76dOZW2gwI/hqdefault.jpg)](https://youtu.be/f76dOZW2gwI)

Full tutorial

[![Watch the video](https://img.youtube.com/vi/qDrXmb2ZRjo/hqdefault.jpg)](https://youtu.be/qDrXmb2ZRjo)

---

## Usage

Import the packages and initialize with your tradingview username and password. If running for first time it will prompt chromedriver download, type 'y' and press enter.

```
from tradingview import TvDatafeed, Interval, symbols

username = 'YourTradingViewUsername'
password = 'YourTradingViewPassword'



tv = TvDatafeed(username, password, chromedriver_path=None)
```

If auto login fails, you can try logging in manually by specifying `auto_login=False`

```
tv = TvDatafeed(auto_login=False)
```

It will open TradingView website, you need to login manually. Once logged in return back to terminal and press 'enter', browser will automatically close. Whichever login method is used, login is required only once.

You may use without logging in, but in that case tradingview may limit the symbols and some symbols might not be available. To use it without logging in

```
tv = TvDatafeed()
```

---

## Getting Data

To download the data use `tv.get_hist` method.

It accepts following arguments and returns pandas dataframe

```
(symbol: str, exchange: str = 'NSE', interval: Interval = Interval.in_daily, n_bars: int = 10, fut_contract: int | None = None) -> DataFrame)
```

for example-

```
# index
nifty_index_data = tv.get_hist(symbol='NIFTY',exchange='NSE',interval=Interval.in_1_hour,n_bars=1000)

# futures continuous contract
nifty_futures_data = tv.get_hist(symbol='NIFTY',exchange='NSE',interval=Interval.in_1_hour,n_bars=1000,fut_contract=1)

# crudeoil
crudeoil_data = tv.get_hist(symbol='CRUDEOIL',exchange='MCX',interval=Interval.in_1_hour,n_bars=5000,fut_contract=1)
```

---

Following timeframes intervals are supported-

`Interval.in_1_minute `

`Interval.in_3_minute `

`Interval.in_5_minute `

`Interval.in_15_minute `

`Interval.in_30_minute `

`Interval.in_45_minute `

`Interval.in_1_hour `

`Interval.in_2_hour `

`Interval.in_3_hour `

`Interval.in_4_hour `

`Interval.in_daily `

`Interval.in_weekly `

`Interval.in_monthly`

---

## Tradingview Symbols

### Search Symbol

To search the symbols

```
symbols.search(symbol='IRCTC')

symbols.search(symbol='IRCTC',exchange='BSE')

>>> [{'symbol': 'IRCTC', 'exchange': 'BSE', 'category': 'STOCKS', 'currency': 'INR', 'description': 'INDIAN RAILWAY CATERING AND TO', 'url': 'http://www.tradingview.com/symbols/BSE-IRCTC'}]

```

### Validate Symbol

You can validate if a symbol exists on tradingview, returns `True` if symbol exists else `False`

```
symbols.validate(symbol='IRCTC',exchange='BSE')
>>> True
```

---

If you face any difficulty you can reset this tvdatafeed using `clear_cache` method. You will need to login again after reset.

```
tv.clear_cache()
```

---

## Troubleshooting

Check this [issue](https://github.com/StreamAlpha/tvdatafeed/issues/26#issuecomment-912619033). A hard reset procedure mainly for linux but works on all platforms.

---
## Read this before creating an issue

Before creating an issue in this library, please follow the following steps.

1. Search the problem you are facing is already asked by someone else. There might be some issues already there, either solved/unsolved related to your problem. Go to [issues](https://github.com/StreamAlpha/tvdatafeed/issues) page, use `is:issue` as filter and search your problem. ![image](https://user-images.githubusercontent.com/59556194/128167319-2654cfa1-f718-4a52-82f8-b0c0d26bf4ef.png)
2. If you feel your problem is not asked by anyone or no issues are related to your problem, then create a new issue.
3. Describe your problem in detail while creating the issue. If you don't have time to detail/describe the problem you are facing, assume that I also won't be having time to respond to your problem.
4. Post a sample code of the problem you are facing. If I copy paste the code directly from issue, I should be able to reproduce the problem you are facing.
5. Before posting the sample code, test your sample code yourself once. Only sample code should be tested, no other addition should be there while you are testing.
6. Have some print() function calls to display the values of some variables related to your problem.
7. Post the results of print() functions also in the issue.
8. Use the insert code feature of github to inset code and print outputs, so that the code is displyed neat. !

9. If you have multiple lines of code, use tripple grave accent ( ``` ) to insert multiple lines of code. [Example:](https://docs.github.com/en/github/writing-on-github/creating-and-highlighting-code-blocks) ![image](https://user-images.githubusercontent.com/59556194/128167963-90edc379-6a15-4363-911f-5bfe1e92ef56.png)


## Historical Data Limit

| Plan | Free | Pro/Pro+ | Premium |
|:-:|:-:|:-:|:-:|
| Limit | 5,000 bars/candles | 10,000 bars/candles | 20,000 bars/candles |

Reference: [I can't see all historical data on resolutions lower than 1 day](https://www.tradingview.com/support/solutions/43000480679-i-can-t-see-all-historical-data-on-resolutions-lower-than-1-day/)

> The length of historical data for any intraday interval (i.e. chart timeframe) is **5,000 bars/candles** (for **Pro and Pro+** account holders it is doubled to **10,000 bars/candles** and for **Premium** holders it's quadrupled to **20,000**) + additionally several bars/candles back to the beginning of the week, month or year (depending on the resolution). Unfortunately, this limit cannot be extended for now due to technical reasons.
>
> If you change the chart interval to daily or daily-based, you will see a longer date range. We display all available data for daily-based intervals.
