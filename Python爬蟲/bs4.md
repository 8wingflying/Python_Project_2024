# Beautiful Soup
- Beautiful Soup 的運作方式就是讀取 HTML 原始碼，自動進行解析並產生一個 BeautifulSoup 物件
- 此物件中包含了整個 HTML 文件的結構樹，有了這個結構樹之後，就可以輕鬆找出任何有興趣的資料

# 安裝

# 範例學習
- [[Python爬蟲] Beautiful Soup 模組](https://ithelp.ithome.com.tw/articles/10340995)

### 範例1:
```python
import requests
from bs4 import BeautifulSoup

response = requests.get('網址')
soup = BeautifulSoup(response.content, 'html.parser')
```
- HTML 解析器:Beautiful Soup 支援多種解析器，每個解析器有其特點
  - Python 標準庫的 html.parser
  - lxml HTML 解析器 ==> BeautifulSoup(markup, "lxml")
  - lxml 的 XML 解析器 ==> BeautifulSoup(markup, "lxml-xml")
  - html5lib 解析器==> BeautifulSoup(markup, "html5lib")

## 使用方法
- Beautiful Soup 提供了多種方法來簡化 HTML 和 XML 文件的解析和數據提取過程。
- find() 和 find_all():
  - find()：找到第一個匹配指定標籤或屬性的元素。
  - find_all()：找到所有匹配指定標籤或屬性的元素。
```
first_paragraph = soup.find('p')
all_paragraphs = soup.find_all('p')
```
- select():使用 CSS 選擇器來選取元素。這對於需要更複雜選擇規則的情況特別有用。
```
articles = soup.select('div.article')
```
- get_text(): 從標籤中提取所有文本內容。
```
text = first_paragraph.get_text()
```
- attributes（屬性）存取:直接從標籤中提取屬性，如 href、id、class 等。
```
link_url = soup.find('a')['href']
```
- children 和 descendants:
  - children：獲取直接子元素。
  - descendants：獲取所有子孫元素。
  - 這些屬性通常用於遍歷元素樹。
- parent 和 parents:
  - parent：獲取直接父元素。
  - parents：獲取所有祖先元素。
  - 這在需要從特定元素向上遍歷文檔樹時非常有用。
- next_sibling 和 previous_sibling:
  - 這些方法可以用來訪問同一層級的下一個或上一個元素。
- string:如果標籤只包含文本，則可以使用 string 屬性直接獲取文本內容。

# 參考資料
- [Beautiful Soup Documentation](https://beautiful-soup-4.readthedocs.io/en/latest/)
- [Python 使用 Beautiful Soup 抓取與解析網頁資料，開發網路爬蟲教學](https://blog.gtwang.org/programming/python-beautiful-soup-module-scrape-web-pages-tutorial/)
