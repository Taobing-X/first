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

然后因为我参加了蓝桥杯和数学建模比赛，也得学习python的算法和用来建模的库，一步一个脚印，慢慢来

**matplotlib库的使用:**

```
import matplotlib.pyplot as plt
from numpy import *
x = arange(-5*pi,5*pi,0.01)
y = sin(x)/x
plt.figure()
plt.plot(x,y,linestyle='-.',color='r',label='sinx/x')
plt.legend()
plt.axis([-20,20,-10,10])
plt.grid(True)
plt.show()
```



**sympy库的使用：**

```
from sympy import *
x = symbols('x')                   #初始化x
y = 2*exp(x)-x*sin(x)
ds1 = diff(y,x,1)                  #求y对于x的一阶导
ds2 = diff(y,x,2)                  #求y对于x的二阶导
zhi = ds2.evalf(subs=({x:0}))      ########求二阶导中当x等于0使的值
z = -100*exp(-0.029*x)+100*x
lim_z1 = limit(z,x,oo)             #求x趋于正无穷+oo时的极限
lim_z2 = limit(z,x,-oo)            #求x趋于负无穷-oo时的极限


x, y = symbols('x y')
z = x ** 2 + y ** 2 - 1
f = idiff(z, y, x)                 #求隐函数

x = symbols('x')
y = cos(x)/(sin(x)*(1+sin(x))**2)
jf = integrate(y,x)                #求y对于x的积原函数
jf = simplify(jf)                  #简化计算结果

y = x**2*sin(x)
jf = integrate(y,(x,0,pi/2))      #求y对于x在(0，2Π)的定积分
jf = simplify(jf)
print("定积分为:",jf)
```

**datetime库的使用：**

```
from datetime import *
y,m,d=map(int,input().split('.'))
d1=datetime(y,m,d)
d2=datetime(y,1,1)
print((d1-d2).days+1)             #求两时间差

#获取当前时间
n1=datetime.now()
#获取时间是星期几(0-6)
n1.weekday()
#获取时间的年份，月份，日子，小时
n1.year  n1.month  n1.day  n1.hour

#跑步锻炼
start=date(2000,1,1)
end=date(2020,10,2)
temp=timedelta(days=1)            #时间差
ans=0
while start != end:
    if start.weekday()==0 or start.day==1:
        ans+=2
    else:
        ans+=1
    start+=temp
print(ans)
```

**字符串操作：**

```
string.isalnum()    #字母或数字
string.isalpha()    #字母
string.isdligit()   #数字
string.isupper()    #大写字母
string.islower()    #小写字母
string.isspace()    #空格
string.upper()		#变大写
string.lower()		#变小写
string.strip()      #消除空格，或指定字符
string.lstrip()     #消除左边的空格，或指定字符
string.rstrip()     #消除右边的空格，或指定字符
string.replace(str1,str2,num=string.count(str1)) #把 string 中的 str1 替换成 str2,如果 num 指定，则替换不超过 num 次.
string.count(str,beg=0,end=len(string)) #返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数
string.encode(encoding='utf-8')  #编码
string.decode(encoding='utf-8')  #解码
string.find(str)    #返回对应str所在的索引下标
srting.index(str)   #与find()方法一样，只不过如果str不在 string中会报一个异常

字符串补齐:
'''
原字符串左侧对齐， 右侧补零:
'''
str.ljust(width,'0') 
input: '789'.ljust(32,'0')
output: '78900000000000000000000000000000'
'''
原字符串右侧对齐， 左侧补零:
方法一：
'''
str.rjust(width,'0') 
input: '798'.rjust(32,'0')
output: '00000000000000000000000000000798'
'''
方法二：
'''
str.zfill(width)
input: '123'.zfill(32)
output:'00000000000000000000000000000123'
'''
方法三：
'''
'%07d' % n
input: '%032d' % 89
output:'00000000000000000000000000000089'
```

