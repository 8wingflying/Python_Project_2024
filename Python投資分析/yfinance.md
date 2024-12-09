# yfinance
- [yfinance GitHub原始碼](https://github.com/ranaroussi/yfinance)
- [yfinance 攻略！Python 下載股票價格數據無難度](https://pythonviz.com/finance/yfinance-download-stock-data/)
- [Python 學習筆記 : 用 yfinance 套件取得股票資料 (二)](https://yhhuang1966.blogspot.com/2022/09/python-yfinance_10.html)
#### 範例1:使用yfinance下載過去一個月內 Apple 股票的歷史價格數據  colab實作OK.20241209
- 範例來源: https://ithelp.ithome.com.tw/articles/10341344
- !pip install  mplfinance yfinance
```python
import yfinance as yf

# 獲取 Apple 股票的數據
apple = yf.Ticker("AAPL")

# 獲取 Apple 股票的歷史價格
hist = apple.history(period="1mo")

# 顯示數據
print(hist)
```

## 實作
- [元大台灣50 (0050.TW)](https://hk.finance.yahoo.com/quote/0050.TW?p=0050.TW&.tsrc=fin-srch)
- GOOGLE COLAB
  - !pip install yfinance
  - 範例程式
```python
import yfinance as yf
a=yf.download('0050.tw',start='2022-12-20',end='2022-12-26')
a
```
- type(a)

## [元大台灣50反1 (00632R.TW)](https://hk.finance.yahoo.com/quote/00632R.TW?p=00632R.TW)
```python
import yfinance as yf

a=yf.download('00632R.tw',period='7d',interval='1m')
a
```
- period == > 7天
- interval  == >每一分鐘

## [yfinance 攻略！Python 下載股票價格數據無難度](https://pythonviz.com/finance/yfinance-download-stock-data/)
- 單一股票
```python
import yfinance as yf

tsm = yf.Ticker(‘TSM’)
tsla = yf.Ticker(‘TSLA’)
tsm.info	
tsm.financials	
tsm.earnings	
tsm.actions	
tsm.history()

```
- 多隻股票下載
```python
b = yf.download('TSM TSLA',start='2016-01-01',end='2021-01-01')
b
```
### 範例2:使用yfinance history 方法
- yfinance 套件中，history 方法是用來獲取股票或其他金融工具的歷史市場數據的主要方式。
- 這個方法返回一個包含了選定時間範圍內的市場數據的 Pandas DataFrame。
- 這些數據通常包括開盤價、最高價、最低價、收盤價和交易量。
```python
import yfinance as yf

# 創建一個股票對象
stock = yf.Ticker("股票代碼")

# 使用 history 方法獲取歷史數據
historical_data = stock.history(period="1mo", interval="1d", start=None, end=None, actions=True, auto_adjust=True, back_adjust=False)
```
- history 方法的參數說明：
  - period：要獲取數據的時間範圍。可以是 "1d", "5d", "1mo", "3mo", "6mo", "1y", "2y", "5y", "10y", "ytd", "max" 等。
  - interval：數據的時間間隔。可以是 "1m", "2m", "5m", "15m", "30m", "60m", "90m", "1h", "1d", "5d", "1wk", "1mo", "3mo" 等。
  - start 和 end：分別指定獲取數據的起始和結束日期。它們應該是字符串（例如 "YYYY-MM-DD"）或 datetime 對象。
  - actions：是否包括股息和股票分割數據。預設為 True。
  - auto_adjust：是否自動調整開盤、收盤、最高和最低價格，以反映股息和股票分割。預設為 True。
  - back_adjust：是否對歷史數據進行回溯調整，以反映股票分割。預設為 False。

```
# 要獲取台積電（代碼 "2330.TW"）過去三個月的每日股票數據：

taiwan_2330 = yf.Ticker("2330.TW")
data = taiwan_2330.history(period="3mo")

# 畫出收盤價圖
data['Close'].plot()
```
### 範例3:使用yfinance Download 方法
- 在 yfinance 套件中，download 方法是一種非常有用的功能，它允許用戶批量下載多個股票的歷史市場數據。
- 這對於需要一次性分析多個股票或資產的用戶來說特別方便。
- 使用 download 方法的基本語法如下：
```
import yfinance as yf

data = yf.download(tickers, start=None, end=None, interval="1d", group_by='ticker', auto_adjust=False, prepost=False, threads=True, proxy=None)

# 參數說明:
# tickers：一個字符串或字符串列表，代表想要下載數據的股票代碼。例如 "AAPL" 或 ["AAPL", "MSFT", "GOOG"]。
# start 和 end：分別代表數據下載的起始和結束日期。它們應該是字符串（例如 "YYYY-MM-DD"）或 datetime 對象。
# interval：數據的時間間隔。可選值包括 "1m"（一分鐘）、"1h"（一小時）、"1d"（一天）、"1wk"（一周）和 "1mo"（一個月）。
# group_by：決定如何組織返回的數據。通常設置為 'ticker'。
# auto_adjust：是否自動調整數據，以反映股息和股票分割。
# prepost：是否包括盤前和盤後的交易數據。
# threads：是否使用多線程來加速下載。
# proxy：用於下載數據的代理服務器。
```
- 範例:下載蘋果公司（AAPL）、微軟公司（MSFT）和谷歌（GOOGL）從 2020 年 1 月 1 日到 2024 年 12 月 1 日的每日股票數據
```python
data = yf.download(["AAPL", "MSFT", "GOOGL"], start="2020-01-01", end="2024-12-1")
```
- 使用 yfinance 的 download 方法下載股票數據時，返回的資料通常是一個 Pandas DataFrame。
- 這個 DataFrame 包含了若干列，每列代表不同的市場數據。以下是這些列的一般說明：
- 列名稱	說明
- Date	日期，表明數據點的具體日期。
- Open	開盤價，指股票在該交易日開市時的價格。
- High	最高價，指股票在該交易日的最高交易價格。
- Low	最低價，指股票在該交易日的最低交易價格。
- Close	收盤價，指股票在該交易日結束時的價格。
- Adj Close	調整後收盤價，將股票分割和股息等因素考慮進去後的收盤價。
- Volume	交易量，表示在該交易日內買賣該股票的總股數。

- 如果您下載多個股票的數據，DataFrame 會稍有不同。
- 在這種情況下，數據通常會按股票代碼進行分組，每個股票代碼下會有上述的數據列。

#### 範例4:使用yfinance下載台灣股票數據  colab實作OK.20241209
- 範例來源: https://ithelp.ithome.com.tw/articles/10341344
- !pip install  mplfinance yfinance
- Period : must be one of ['1d', '5d', '1mo', '3mo', '6mo', '1y', '2y', '5y', '10y', 'ytd', 'max']
```
import yfinance as yf
import mplfinance as mpf

# 下載台灣 2330 (台積電) 的股票數據
taiwan_2330 = yf.Ticker("2330.TW")
df = taiwan_2330.history(period="max")

# 檢查數據是否成功下載
if df.empty:
    print("股票數據下載失敗或沒有數據。")
else:
    # 繪製 K 線圖
    mpf.plot(df, type='candle', style='charles', title='2330', volume=True)
```
- mpf.plot重要參數說明
  - df:
    - mplfinance 輸入的數據必須是 pandas.DataFrame 類型
    - 對數據格式的要求，必須含有 ‘Open’ , ‘High’ , ‘Low’ , ‘Close’ , ‘Volume’，
    - 列索引為 pandas.DatetimeIndex 格式、名稱為 ‘Date’。
  - type='candle'
  - style='charles'
  - title='2330'
  - volume=True ==> 顯示成交量
  - mav ==> mpf.plot(data, type='line', mav=(2, 5, 10))

## 實作
- [元大台灣50 (0050.TW)](https://hk.finance.yahoo.com/quote/0050.TW?p=0050.TW&.tsrc=fin-srch)
- GOOGLE COLAB
  - !pip install yfinance
  - 範例程式
```python
# 元大台灣50 (0050.TW)
import yfinance as yf
a=yf.download('0050.tw',start='2022-12-20',end='2022-12-26')
a
type(a)

# [元大台灣50反1 (00632R.TW)](https://hk.finance.yahoo.com/quote/00632R.TW?p=00632R.TW)

a=yf.download('00632R.tw',period='7d',interval='1m')
a

## period == > 7天
## interval  == >每一分鐘
```
#### [yfinance 攻略！Python 下載股票價格數據無難度](https://pythonviz.com/finance/yfinance-download-stock-data/)
- 單一股票
```python
import yfinance as yf

tsm = yf.Ticker(‘TSM’)
tsla = yf.Ticker(‘TSLA’)
tsm.info	
tsm.financials	
tsm.earnings	
tsm.actions	
tsm.history()
```
- 多隻股票下載
```python
b = yf.download('TSM TSLA',start='2016-01-01',end='2021-01-01')
b
```
# 參考資料
- [Python量化交易——mplfinance最佳实践：动态交互式高级K线图(蜡烛图)【源码+详解】](https://blog.csdn.net/Shepherdppz/article/details/117575286)
- [Plot Stock Chart Using mplfinance in Python](https://plainenglish.io/blog/plot-stock-chart-using-mplfinance-in-python-9286fc69689)
