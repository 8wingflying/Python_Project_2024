# 1022 urllib
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
## urllib2.py
```
import urllib.request

response = urllib.request.urlopen('https://www.python.org')
print(response.status)
print(response.getheaders())
# print(response.getheader('Server'))
print(response.getheader('Content-Length'))
```
```
print(response.getheader('Server'))
呼叫getheader 方法並傳遞一個參數 Content-Length
==> 獲取response 表頭的 Content-Length 值
```
## urllib3.py ==> 使用error模組
```python
from urllib import request, error
try:
    response = request.urlopen('http://cuiqingcai.com/index.htm')
except error.URLError as e:
    print(e.reason)
```
## urllib4.py ==> 使用error模組
```python
from urllib import request,error
try:
    response = request.urlopen('http://cuiqingcai.com/index.htm')
except error.HTTPError as e:
    print(e.reason, e.code, e.headers, sep='\n')
```
## 開啟chrome 開發人員工具 == > F12
# request 模組 參考 [3.2　使用 requests](https://github.com/MyDearGreatTeacher/Python3WebSpider/blob/master/3.2-%E4%BD%BF%E7%94%A8requests.md)

## request1.py
- HTTP/ 1.1 八大方法(Method) == > GET POST PUT DELETE HEAD OPTIONS
```python
import requests

r = requests.get('https://www.baidu.com/')
print(type(r))
print(r.status_code)
print(type(r.text))
print(r.text[:1000])
print(r.cookies)
```
```python
r = requests.post('http://httpbin.org/post')  
r = requests.put('http://httpbin.org/put')  
r = requests.delete('http://httpbin.org/delete')  
r = requests.head('http://httpbin.org/get')  
r = requests.options('http://httpbin.org/get')
```
## request2.py
```python
import requests  

r = requests.get('http://httpbin.org/get')  
print(r.text)
```
## request3.py
```python

```
## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```

## request3.py
```python

```
