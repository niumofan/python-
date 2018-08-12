#1 普通爬取
import requests

url = ""
try:
    r = requests.get(url)
    r.raise_for_status()
    r.encoding = r.apparent_encoding
    print(r.text[:])
except:
    print("爬取失败")
    
    
#2 伪装成浏览器爬取
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


#4 从往上爬取图片
例：
import requests
import os

url = "http://www.artsbj.com/uploadfile/2017/1208/20171208090726952.jpg"
root = "E//图片//"
path = root + url.split[-1]

try:
    if not os.path.exists(root):
        os.mkdir(root)
    if not os.path.exists(path):
        r = requests.get(url)
        with open(path, "wb") as f:
            f.write(r.content)
        f.close()
        print("图片保存成功")
    else:
        print("文件已存在")
except:
    print("爬取失败")
    

#5 查询IP地址
例：
import requests

url = "http://m.ip138.com/ip.asp"
ip = input("请输入IP地址")
kv = {'ip':ip}

try:
    r = requests.get(url, params = kv)
    r.raise_for_status();
    r.encoding = r.apparent_encoding
    print(r.text[-500:])
except:
    print("爬取失败")
