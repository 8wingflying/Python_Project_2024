# FINMIND模組
- [FinMind 金融 X 大數據](https://finmindtrade.com/)
- [Quick start with FinMind Finance data API](https://finmind.github.io/quickstart/)
- [FinMind拿資料，只提供部分免費功能!](https://ithelp.ithome.com.tw/articles/10343838)
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
