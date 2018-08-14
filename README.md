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


#6 中国大学排名爬取
以交通大学最好大学排名为例：
import requests
from bs4 import BeautifulSoup
import bs4

def getHTMLText(url):
    try:
        r = requests.get(url, timeout=30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return ""

def fillUnivList(ulist, html):
    soup = BeautlfulSoup(html, "html.parser")
    for tr in soup.find('tbody').children:
        if isinstance(tr, bs4.element.Tag):
            tds = tr('td')
            ulist.append([tds[0].string, tds[1].string, tds[3].string])

def printUnivList(ulist, num):
    tplt = "{0:^10}\t{1:{3}^10}\t{2:^10}"
    print(tplt.format("排名", "学校名称", "总分",chr(12288))) #chr(12288)是中文的空格符，防止中西文输出不美观
    for i in range(num):
        u = ulist[i]
        print(tplt.format(u[0], u[1], u[2], chr(12288)))
    
def main():
    url = "http://www.zuihaodaxue.com/zuihaodaxuepaiming2016.html"
    uinfo = []
    html = getHTMLText(url)
    fillUnivList(uinfo, html)
    printUnivList(uinfo, 20)

main()

输出:
    排名    	　　学校名称　　　	   总分    
    1     	　　　清华大学　　　	   95.9   
    2     	　　　北京大学　　　	   82.6   
    3     	　　　浙江大学　　　	    80    
    4     	　　上海交通大学　　	   78.7   
    5     	　　　复旦大学　　　	   70.9   
    6     	　　　南京大学　　　	   66.1   
    7     	　中国科学技术大学　	   65.5   
    8     	　哈尔滨工业大学　　	   63.5   
    9     	　　华中科技大学　　	   62.9   
    10    	　　　中山大学　　　	   62.1   
    11    	　　　东南大学　　　	   61.4   
    12    	　　　天津大学　　　	   60.8   
    13    	　　　同济大学　　　	   59.8   
    14    	　北京航空航天大学　	   59.6   
    15    	　　　四川大学　　　	   59.4   
    16    	　　　武汉大学　　　	   59.1   
    17    	　　西安交通大学　　	   58.9   
    18    	　　　南开大学　　　	   58.3   
    19    	　　大连理工大学　　	   56.9   
    20    	　　　山东大学　　　	   56.3   


#7 爬取股票数据
以百度股票网和东方财富网为例：
import requests
import re
from bs4 import BeautifulSoup
import traceback

def getHTMLText(url):
    try:
        r = requests.get(url)
        r.raise_foe_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return ""
    
def getStockList(lst, stockURL):
    html = getHTMLText(stockURL)
    soup = BeautifulSoup(html, "html.parser")
    a = soup.find_all('a')
    for i in a:
        try:
            href = a.attrs['href']
            lst.append(re.findall(r'[s][hz]\d{6}', href)[0])
        except:
            continue
        
def getStockInfo(lst, stockURL, fpath):
    count = 0
    for stock in lst:
        url = stockURL + stock + ".html"
        html = getHTMLText(url)
        try:
            if html == "":
                continue
            infoDict = {}
            soup = BeautifulSoup(html, "html.parser")
            stockInfo = soup.find('div', attrs={'class':'stock-bets'})

            name = stockInfo.find_all(attrs={'class':'bets-name'})[0]
            infoDict.update({'股票名称':name.text.split()[0]})

            keyList = stockInfo.find('dt')
            valueList = stockInfo.find_all('dd')
            for i in range(len(keyList)):
                key = keyList[i].text
                val = valueList[i].text
                infoDict[key] = val

            with open(fpath, 'a', encoding='utf-8') as f:
                f.write(str(infoDict) + '\n')
                count += 1
                print("\r当前进度:{:.2f}%".format(count*100/len(lst)), end = '')
        except:
            count += 1
            print("\r当前进度:{:.2f}%".format(count*100/len(lst)), end = '')
            traceback.print_exc()
            continue
def main():
    stock_list_url = "http://quote.eastmoney.com/stocklist.html"
    stock_info_url = "https://gupiao.baidu.com/stock/"
    output_file = "E//Python//程序//BaiduStockInfo.txt"
    slist = []
    getStockList(slist, stock_list_url)
    getStockInfo(slist, stock_info_url, output_file)

main()
