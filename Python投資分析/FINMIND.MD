# FINMIND模組
- [FinMind 金融 X 大數據](https://finmindtrade.com/)
- [Quick start with FinMind Finance data API](https://finmind.github.io/quickstart/)
- [FinMind拿資料，只提供部分免費功能!](https://ithelp.ithome.com.tw/articles/10343838)
- [說明文件|官方網址](https://finmind.github.io/)

- Google Colab安裝 ==> !pip install FinMind

#### 範例:捉 0050 資料，開始時間寫 2000-01-01 (0050 上市時間是 2003-06)
- [如何使用Python取得歷史股價，簡介yfinance、ffn、FinMind](https://havocfuture.tw/blog/python-stock-history)
```python
from FinMind.data import DataLoader

stock_no = '0050'
dl = DataLoader()
stock_data = dl.taiwan_stock_daily(stock_id=stock_no, start_date='2000-01-01')
stock_data.head()
```
#### 範例:台積電（2330）下載台股歷史收盤數據
- [[Day 04] 透過FinMind取得台股收盤資訊]()

```PYTHON
from FinMind.data import DataLoader

api = DataLoader()
api.login_by_token(api_token="Your_API_Key")

stock_data = api.taiwan_stock_daily(
    stock_id="2330", 
    start_date="2020-01-01", 
    end_date="2024-09-18"
)
print(stock_data)
```

```PYTHON
from FinMind.data import DataLoader

api = DataLoader()
api.login_by_token(api_token="Your_API_Key")

df = api.taiwan_stock_institutional_investors(
    stock_id="2330",
    start_date='2020-04-01',
    end_date='2024-09-18'
)
print(df)
```
```
stock_data.to_csv("TSMC_stock_data.csv", index=False)
```

```PYTHON
import pandas as pd

# Read Your CSV
df = pd.read_csv(r'C:\iThome\TSMC_stock_data.csv')

def calculate_ma(data, window):
    return data.rolling(window=window).mean()

ma_window = 50  # MA Length

df[f'MA_{ma_window}'] = calculate_ma(df['close'], ma_window)

df.to_csv('TSMC_stock_data_with_MA.csv', index=False)
```


### 範例
- [[FinMind Data] 台灣大盤融資資維持率](https://medium.com/finmind/finmind-data-%E5%8F%B0%E7%81%A3%E5%A4%A7%E7%9B%A4%E8%9E%8D%E8%B3%87%E8%B3%87%E7%B6%AD%E6%8C%81%E7%8E%87-4bfce625483d)
- [程式碼](https://gist.github.com/machineCYC/955250c19a7d53ad19ec884405589967#file-gistfile1-txt)
```PYTHON
# 計算大盤 2022-06-29 融資維持率

import numpy as np
import pandas as pd
import requests

token = ""
url = "https://api.finmindtrade.com/api/v4/data"

# filter stock_id
parameter = {
    "dataset": "TaiwanStockInfo",
    "token": token, # 參考登入，獲取金鑰
}
data = requests.get(url, params=parameter)
TaiwanStockInfo = data.json()
TaiwanStockInfo = pd.DataFrame(TaiwanStockInfo['data'])
TaiwanStockInfo['is_bt'] = TaiwanStockInfo['stock_name'].map(lambda x: True if '乙特' in x else False)
TaiwanStockInfo['is_at'] = TaiwanStockInfo['stock_name'].map(lambda x: True if '甲特' in x else False)

mask = (
    TaiwanStockInfo['type'].isin(['twse']) & 
    ~TaiwanStockInfo['industry_category'].isin(['ETF', '大盤']) &
    ~TaiwanStockInfo['is_bt'] &
    ~TaiwanStockInfo['is_at']
)
print(TaiwanStockInfo[mask].tail())
stock_type_list = TaiwanStockInfo[mask]['stock_id'].unique()

# 獲得個股每日收盤價
parameter = {
    "dataset": "TaiwanStockPrice",
    "start_date": "2022-06-29",
    "token": token, # 參考登入，獲取金鑰
}
resp = requests.get(url, params=parameter)
TaiwanStockPrice = resp.json()
TaiwanStockPrice = pd.DataFrame(TaiwanStockPrice["data"])
print(TaiwanStockPrice[["date", "stock_id", "close"]].head())

# 獲得個股每日融資張數
parameter = {
    "dataset": "TaiwanStockMarginPurchaseShortSale",
    "start_date": "2022-06-29",
    "token": token, # 參考登入，獲取金鑰
}
resp = requests.get(url, params=parameter)
TaiwanStockMarginPurchaseShortSale = resp.json()
TaiwanStockMarginPurchaseShortSale = pd.DataFrame(TaiwanStockMarginPurchaseShortSale["data"])
TaiwanStockMarginPurchaseShortSale = TaiwanStockMarginPurchaseShortSale[
    ['date', 'stock_id', 'MarginPurchaseTodayBalance']
]
print(TaiwanStockMarginPurchaseShortSale.head())


# 獲得大盤融資餘額
parameter = {
    "dataset": "TaiwanStockTotalMarginPurchaseShortSale",
    "start_date": "2022-06-29",
    "token": token, # 參考登入，獲取金鑰
}
data = requests.get(url, params=parameter)
TaiwanStockTotalMarginPurchaseShortSale = data.json()
TaiwanStockTotalMarginPurchaseShortSale = pd.DataFrame(TaiwanStockTotalMarginPurchaseShortSale['data'])
TaiwanStockTotalMarginPurchaseShortSale = TaiwanStockTotalMarginPurchaseShortSale[TaiwanStockTotalMarginPurchaseShortSale['name']=='MarginPurchaseMoney']
TaiwanStockTotalMarginPurchaseShortSale = TaiwanStockTotalMarginPurchaseShortSale[TaiwanStockTotalMarginPurchaseShortSale['date']=='2022-06-29']
print(TaiwanStockTotalMarginPurchaseShortSale[["date", "TodayBalance"]].tail())

# 計算2022-06-29 大盤融資維持率
merge_data = pd.merge(TaiwanStockPrice, TaiwanStockMarginPurchaseShortSale, on=['date', 'stock_id'], how='left')
merge_data['MarginPurchaseTotalValue'] = merge_data['MarginPurchaseTodayBalance'] * merge_data['close'] * 1000
value = merge_data[merge_data['stock_id'].isin(stock_type_list)]['MarginPurchaseTotalValue'].sum()
print(f"2022-06-29 大盤融資維持率:{value / TaiwanStockTotalMarginPurchaseShortSale['TodayBalance'].values[0]}")

```
