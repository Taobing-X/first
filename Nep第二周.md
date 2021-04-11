# Nepnep学习报告 web第一周
又是没有web提纲的一周，还是比较迷茫要怎么学web

就接着学python了，不管web要学啥，编程能力肯定都是必须哒

**1.Requests模块例子**

例：

判断状态码是不是 200
```
import requests

try:
  url = 'https://www.baidu.com'

  r = requests.get(url)

  if r.status_code == 200:
    print('hello')
except:
  print('error')
```

