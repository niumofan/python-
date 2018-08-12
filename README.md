#1
import requests

url = ""
try:
    r = requests.get(url)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[:])
except:
    print("爬取失败")
    
    
#2
import requests
url = ""
try:
    kv = {'user-agent':'Mozilla/5.0'}
    r = requests.get(url, headers = kv)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[:])
except:
    print("爬取失败")

#3  百度搜索
import requests
url = "http://www.baidu.com/s"
keyword = input("请输入您要搜索的关键词：")
kv = {'wd':keyword}
try:
    r = requests.get(url, params = kv)
    r.raise_for_status()
    print("网址链接：", r.request.url)
    print("长度：", len(r.text))
except:
    print("搜索失败")
