# 1022
- 驗證本地端是否已安裝好套件
```
python
Python 3.10.6 (tags/v3.10.6:9c7b4bd, Aug  1 2022, 21:53:49) [MSC v.1932 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests
>>> import selenium
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'selenium'
>>>
```
- 安裝:pip3 install requests 
- 安裝:pip3 install selenium
# urllib
- urllib 是 Python 內置的 HTTP 請求庫
- 不需要額外安裝即可使用。
- urllib包含如下 4 個模組:
  - request：它是最基本的 HTTP 請求模組，可用來類比發送請求。只需要給庫方法傳入 URL 以及額外的參數，就可以模擬實現這個過程了
  - error：異常處理模組，如果出現請求錯誤，我們可以捕獲這些異常，然後進行重試或其他操作以保證程式不會意外終止。
  - parse：一個工具模組，提供了許多 URL 處理方法，比如拆分、解析和合併等。
  - robotparser：主要用來識別網站的 robots.txt 檔，然後判斷哪些網站可以爬，哪些網站不可以爬，它其實用得比較少。
## urllib1.py
```python
import urllib.request

response = urllib.request.urlopen('https://www.python.org')
print(response.read().decode('utf-8'))
```

# request 模組

## request1.py
```python
import requests

r = requests.get('https://www.baidu.com/')
print(type(r))
print(r.status_code)
print(type(r.text))
print(r.text[:1000])
print(r.cookies)
```

