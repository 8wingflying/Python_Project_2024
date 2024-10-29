## [資料來源](https://github.com/Python3WebSpider/Python3WebSpider/blob/master/3.4-%E7%88%AC%E5%8F%96%E7%8C%AB%E7%9C%BC%E7%94%B5%E5%BD%B1%E6%8E%92%E8%A1%8C.md)

```python
import json  
import requests  
from requests.exceptions import RequestException  
import re  
import time  

def get_one_page(url):  
    try:  
        headers = {'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_3) AppleWebKit/537.36 (KHTML, like    Gecko) Chrome/65.0.3325.162 Safari/537.36'  
        }

        response = requests.get(url, headers=headers)  
        if response.status_code == 200:  
            return response.text  
        return None  
    except RequestException:  
        return None  

def parse_one_page(html):  
   pattern = re.compile('<dd>.*?board-index.*?>(\d+)</i>.*?data-src="(.*?)".*?name"><a' '.*?>(.*?)</a>.*?star">(.*?)</p>.*?releasetime">(.*?)</p>'  '.*?integer">(.*?)</i>.*?fraction">(.*?)</i>.*?</dd>', re.S)  

   items = re.findall(pattern, html)  
   for item in items:  
        yield {'index': item[0],  
            'image': item[1],  
            'title': item[2],  
            'actor': item[3].strip()[3:],  
            'time': item[4].strip()[5:],  
            'score': item[5] + item[6]  
        }  

def write_to_file(content):  
    with open('result.txt', 'a', encoding='utf-8') as f:  
        f.write(json.dumps(content, ensure_ascii=False) + '\n')  

def main(offset):  
    url = 'http://maoyan.com/board/4?offset=' + str(offset)  
    html = get_one_page(url)  
    for item in parse_one_page(html):  
        print(item)  
        write_to_file(item)  

if __name__ == '__main__':  
    for i in range(10):  
        main(offset=i * 10)  
        time.sleep(1)
```
