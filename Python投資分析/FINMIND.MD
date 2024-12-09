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
