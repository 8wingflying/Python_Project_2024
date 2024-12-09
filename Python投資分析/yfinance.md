# yfinance

# 範例2:使用yfinance下載台灣股票數據  colab實作OK.20241209
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

# 參考資料
- [Python量化交易——mplfinance最佳实践：动态交互式高级K线图(蜡烛图)【源码+详解】](https://blog.csdn.net/Shepherdppz/article/details/117575286)
- [Plot Stock Chart Using mplfinance in Python](https://plainenglish.io/blog/plot-stock-chart-using-mplfinance-in-python-9286fc69689)
