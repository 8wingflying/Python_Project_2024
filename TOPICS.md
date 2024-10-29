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
## request2.py  ==> 使用HTTP GET 方法
```python
import requests  

r = requests.get('http://httpbin.org/get')  
print(r.text)
```
## request3.py ==> 使用HTTP GET 方法 + 傳遞參數
```python
import requests 
r = requests.get('http://httpbin.org/get?name=germey&age=22')

print(r.text)
```
## request4.py ==> 更多傳遞參數 == >使用HTTP GET 方法 + params 
```python
import requests  

data = {  
    'name': 'germey',  
    'age': 22  
}

r = requests.get("http://httpbin.org/get", params=data)  
print(r.text)
```

## request5.py ==> 略  re == regular expression
```python
import requests
import re

headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/52.0.2743.116 Safari/537.36'
}
r = requests.get("https://www.zhihu.com/explore", headers=headers)
pattern = re.compile('explore-feed.*?question_link.*?>(.*?)</a>', re.S)
titles = re.findall(pattern, r.text)
print(titles)
```

## request6.py == > 抓取 binary (音樂 | 影片 | 惡意程式 | ....) ==> 16進位的呈現
```python
import requests

r = requests.get("https://github.com/favicon.ico")
print(r.text)
print(r.content) # 16進位的呈現
```

## request7.py
```python
import requests

r = requests.get("https://github.com/favicon.ico")
with open('A888168.ico', 'wb') as f:
    f.write(r.content)
```

## request8.py ==> 使用HTTP POST 方法 + 傳遞參數
```python
import requests

data = {'name': 'germey', 'age': '22'} # Python 字典
r = requests.post("http://httpbin.org/post", data=data)
print(r.text)
```

## request9.py
```python
import requests

r = requests.get('http://www.jianshu.com') # r ==> response header
print(type(r.status_code), r.status_code)
print(type(r.headers), r.headers)
print(type(r.cookies), r.cookies)
print(type(r.url), r.url)
print(type(r.history), r.history)
```

## request10.py
```python
import requests

r = requests.get('http://www.jianshu.com')
exit() if not r.status_code == requests.codes.ok else print('Request Successfully')
```
```
if not r.status_code == requests.codes.ok
   
else
   print('Request Successfully')
```

## http status code
```python
# 資訊性狀態碼  
100: ('continue',),  
101: ('switching_protocols',),  
102: ('processing',),  
103: ('checkpoint',),  
122: ('uri_too_long', 'request_uri_too_long'),  

# 成功狀態碼  
200: ('ok', 'okay', 'all_ok', 'all_okay', 'all_good', '\\o/', '✓'),  
201: ('created',),  
202: ('accepted',),  
203: ('non_authoritative_info', 'non_authoritative_information'),  
204: ('no_content',),  
205: ('reset_content', 'reset'),  
206: ('partial_content', 'partial'),  
207: ('multi_status', 'multiple_status', 'multi_stati', 'multiple_stati'),  
208: ('already_reported',),  
226: ('im_used',),  

# 重定向狀態碼  
300: ('multiple_choices',),  
301: ('moved_permanently', 'moved', '\\o-'),  
302: ('found',),  
303: ('see_other', 'other'),  
304: ('not_modified',),  
305: ('use_proxy',),  
306: ('switch_proxy',),  
307: ('temporary_redirect', 'temporary_moved', 'temporary'),  
308: ('permanent_redirect',  
      'resume_incomplete', 'resume',), # These 2 to be removed in 3.0  

# 用戶端錯誤狀態碼  
400: ('bad_request', 'bad'),  
401: ('unauthorized',),  
402: ('payment_required', 'payment'),  
403: ('forbidden',),  
404: ('not_found', '-o-'),  
405: ('method_not_allowed', 'not_allowed'),  
406: ('not_acceptable',),  
407: ('proxy_authentication_required', 'proxy_auth', 'proxy_authentication'),  
408: ('request_timeout', 'timeout'),  
409: ('conflict',),  
410: ('gone',),  
411: ('length_required',),  
412: ('precondition_failed', 'precondition'),  
413: ('request_entity_too_large',),  
414: ('request_uri_too_large',),  
415: ('unsupported_media_type', 'unsupported_media', 'media_type'),  
416: ('requested_range_not_satisfiable', 'requested_range', 'range_not_satisfiable'),  
417: ('expectation_failed',),  
418: ('im_a_teapot', 'teapot', 'i_am_a_teapot'),  
421: ('misdirected_request',),  
422: ('unprocessable_entity', 'unprocessable'),  
423: ('locked',),  
424: ('failed_dependency', 'dependency'),  
425: ('unordered_collection', 'unordered'),  
426: ('upgrade_required', 'upgrade'),  
428: ('precondition_required', 'precondition'),  
429: ('too_many_requests', 'too_many'),  
431: ('header_fields_too_large', 'fields_too_large'),  
444: ('no_response', 'none'),  
449: ('retry_with', 'retry'),  
450: ('blocked_by_windows_parental_controls', 'parental_controls'),  
451: ('unavailable_for_legal_reasons', 'legal_reasons'),  
499: ('client_closed_request',),  

# 服務端錯誤狀態碼  
500: ('internal_server_error', 'server_error', '/o\\', '✗'),  
501: ('not_implemented',),  
502: ('bad_gateway',),  
503: ('service_unavailable', 'unavailable'),  
504: ('gateway_timeout',),  
505: ('http_version_not_supported', 'http_version'),  
506: ('variant_also_negotiates',),  
507: ('insufficient_storage',),  
509: ('bandwidth_limit_exceeded', 'bandwidth'),  
510: ('not_extended',),  
511: ('network_authentication_required', 'network_auth', 'network_authentication')

```

## request3.py
```python

```

## request3.py
```python

```
