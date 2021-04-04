# Nepnep学习报告 web第一周
因为web提纲还没出来，方向还不是挺清晰，就先把python好好补一下

# 1. requests.get()


  这个我们最常见，也是用的最多的，

  基本使用方法：

```
r = request.get(url,params,kwargs)
这句代码是构造一个服务器请求request，返回一个包含服务器资源的response对象。
```

  其中：

  url: 需要爬取的网站地址。

  params: 翻译过来就是参数， url中的额外参数，字典或者字节流格式，可选。

  kwargs : 12个控制访问的参数
  
  kwargs有以下参数：

    params：字典或字节序列， 作为参数增加到url中，

    使用这个参数可以把一些键值对以?key1=value1&key2=value2的模式增加到url中

例如：
```
>>> import requests  #  导入模块
>>> url = 'http://www.xxxxxxxx.com/index.php'  #  设置 url
>>> payload = {'key1': 'values', 'key2': 'values'}
>>> r = requests.get(url, params=payload) 
>>> print(r.url)
>>> # 输出 http://www.xxxxxxxx.com/index.php?key2=values&key1=values
>>> print(r.status_code)  # 输出 200 （状态码）

这里 r 是自定义的变量名，用来接收返回值 response
```



 json：  json格式的数据， json合适在相关的html，http相关的web开发中非常常见， 也是http最经常使用的数据格式，

 他是作为内容部分可以向服务器提交。

例如：
```
url = 'http://www.xxxxxxxx.com/index.php'
payload = {'key1': 'value1'} 
r = requests.post(url, json=payload)
print(r.json)
>>> # 输出  bound method Response.json of <Response [200]>
```
 headers： 字典是http的相关语，对应了向某个url访问时所发起的http的头字段，

  可以用这个字段来定义http的访问头，可以模拟任何浏览器来对url发起访问。

例如：
```
url = 'http://www.xxxxxxxx.com/index.php'
header = {'user-agent': 'Chrome/10'} 
r = requests.get(url, headers=header)
print(r.headers)
```
   cookies：字典或CookieJar，指的是从http中解析cookie

   auth：元组，用来支持http认证功能

   files：字典， 是用来向服务器传输文件时使用的字段。

例如：
```
url = 'http://www.xxxxxxxx.com/index.php'
file = {'files': open('data.txt', 'rb')} 
r = requests.post(url, files=file)
print(r.text)
```
   timeout: 用于设定超时时间， 单位为秒，当发起一个get请求时可以设置一个timeout时间，

   如果在timeout时间内请求内容没有返回， 将产生一个timeout的异常。

   proxies：字典， 用来设置访问代理服务器。
   
   allow_redirects: 开关， 表示是否允许对url进行重定向， 默认为True。
    
   stream: 开关， 指是否对获取内容进行立即下载， 默认为True。
   
   verify：开关， 用于认证SSL证书， 默认为True。
   
   cert： 用于设置保存本地SSL证书路径
   
  ***Response对象属性：***
   
属性 	                  说明

r.status_code 	      http请求的返回状态，若为200则表示请求成功。

r.text 	              http响应内容的字符串形式，即返回的页面内容

r.encoding 	          从http header 中猜测的相应内容编码方式

r.apparent_encoding 	从内容中分析出的响应内容编码方式（备选编码方式）

r.content 	          http响应内容的二进制形式


# 2. requests.head()

head 获取html头部信息的方法 。

例如：
```
import requests

url = "https://www.xxxxxxxx.com"

r = requests.get(url)

print(r.headers)
```
# 3. requests.post()

发送post请求

POST 方法被用于请求源服务器接受请求中的实体作为请求资源的一个新的从属物

例如：
```
>>> payload = {"key1":"value1","key2":"value2"}
>>> r = requests.post("http://www.xxxxxxxx.com/index.php",data=payload)
>>> print(r.text)
{
  "args": {}, 
  "data": "", 
  "files": {}, 
  "form": {
    "key1": "value1", 
    "key2": "value2"
  }, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Connection": "close", 
    "Content-Length": "23", 
    "Content-Type": "application/x-www-form-urlencoded", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.18.4"
  }, 
  "json": null, 
  "origin": "192.168.1.2", 
  "url": "http://www.xxxxxxxx.com/index.php"
}
```
向url post 一个字符串，自动编码为data
```
>>>r=requests.post("http://www.xxxxxxxx.com/index.php",data='hello world')
>>>print(r.text)
{
  "args": {}, 
  "data": "hello world", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept": "*/*", 
    "Accept-Encoding": "gzip, deflate", 
    "Connection": "close", 
    "Content-Length": "10", 
    "Host": "httpbin.org", 
    "User-Agent": "python-requests/2.18.4"
  }, 
  "json": null, 
  "origin": "192.168.1.2", 
  "url": "http://www.xxxxxxxx.com/index.php"
}
```
