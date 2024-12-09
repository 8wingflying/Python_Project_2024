# mplfinance 
- matplotlib utilities for the visualization, and visual analysis, of financial data

## 參考資料
- [Python 學習筆記 : 用 mplfinance 套件繪製金融圖表 (一) K 線圖](https://yhhuang1966.blogspot.com/2022/09/python-mplfinance.html)
- [mplfinance模块详解](https://www.cnblogs.com/yuyanc/p/16388190.html)

### 繪製台灣股市
- 繪製台灣股市的 K 線圖須先用 make_marketcolors() 與 make_mpf_style() 函式自訂樣式字典 :
```python
color=mpf.make_marketcolors(up='red', down='green', inherit=True)   
font={'font.family': 'Microsoft JhengHei'}   
style=mpf.make_mpf_style(base_mpf_style='default', marketcolors=color, rc=font)     

# 然後在呼叫 plot() 時將樣式字典傳給 style 參數 :

mpf.plot(df, type='candle', title='台灣五十(0050)', style=style)
```
