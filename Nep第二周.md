# Nepnep学习报告 web第二周
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


# os模块：

os 是一个获取和处理文件，目录 的模块，

下面列举一些比较常用的方法。
**os.access()**

作用：查看文件是否有指定权限，有则返回True否则返回flase

语法： os.access(path, mode)

path 文件路径

mode 参数有：

F_OK (是否存在)

R_OK (可读)

W_OK (可写)

X_OK (可执行)
```
例：

>>> import os
>>> r = os.access('/python/test.py',os.F_OK)  #  判断文件是否存在
>>> print(r)
>>> # 输出 True
```
**os.getcwd()**

作用：获取当前目录，即当前python脚本工作的目录路径
```
例：

>>> import os
>>> r = os.getcwd()  #  获取路径
>>> print(r)
>>> # 输出 C:\Users\administrator\Desktop
```
**os.listdir()**

作用：获取指定目录下文件和目录的名称，跟 dir 命令一样
```
例：

>>> import os
>>> r = os.listdir('C:/')  #  获取目录和文件名
>>> print(r)
```
**os.chdir()**

作用：切换工作目录到指定的路径下，成功返回True，失败返回False
```
例：

>>> import os
>>> r = os.chdir('../')  #  切换到上一级目录
>>> print(r)
```
**os.mkdir(path, mode=511)**

作用：创建一个目录，并指定访问权限，在windows平台下, mode参数将会被忽略

默认的访问权限为 511，表示8进制的 0o777，即拥有者，用户组和其他用户均具有读、写和执行的权限。
```
例：

>>> import os
>>> r = os.mkdir('D:/test')  #  在D盘下创建一个test的目录
>>> print(r)
```
**os.makedirs(name, mode=511, exist_ok=False)**

作用：递归地创建目录并设置访问权限，类似于linux中的 mkdir -p

权限跟上面一样
```
例：

>>> import os
>>> r = os.makedirs('D:/test/test')  #  在D盘下创建一个test的目录,然后在test目录再创建一个test目录
>>> print(r)
```
**os.rmdir(path)**

作用：删除指定的目录，若目录非空及里面有文件，则抛出OSError异常。
```
>>> import os
>>> r = os.rmdir('D:/test')  #  删除D盘下的test目录
>>> print(r)
```
**os.removedirs(path)**

作用：递归删除指定的目录。

若指定的是一个文件，则引发 NotADirectoryError 异常

若指定的目录不为空，则引发OSError异常。
```
例：

>>> import os
>>> r = os.removedirs('D:/test/test')  #  递归删除在D盘下的两个test目录
>>> print(r)
```
**os.remove(path)**

作用：删除指定的文件。若 path 为一个目录，则引 PermissionError 异常
```
例：

>>> import os
>>> r = os.remove('D:/test.txt')  #  删除在D盘下的test.txt文件
>>> print(r)
```
**os.rename(src, dst)**

作用：重命名文件或目录，如果dst是一个存在的目录, 将抛出OSError。

src – 要修改的目录名

dst – 修改后的目录名
```
例：

>>> import os
>>> r = os.rename('D:/test','D:/test2')  #  将D盘下的test目录重命名为test2
>>> print(r)
```
**os.chown(path, uid, gid)**

作用：用于更改文件所有者，如果不修改可以设置为 -1

path – 设置权限的文件路径

uid – 所属用户 ID

gid – 所属用户组 ID
```
例如：

>>> import os
>>> r = os.chown('test.txt',0,0) # 设置文件的UID为0，root用户，GID为0，root组
>>> print(r)
```
**os.system(“bash command”)**

运行shell命令，直接显示
```
例如：

>>> import os
>>> r = os.system('dir')  # 执行 dir 命令 
>>> print(r)
```


# sys模块：

sys.argv 接收命令行参数，生成一个List，第一个元素是程序本身路径
```
例如：

>>> test.py https://www.baidu.com/ 
>>> import sys
>>> r = sys.argv[0]  # 获取脚本名
>>> print(r)  # 输出 test
>>> r2 = sys.argv[1]  # 获取第一个参数
>>> print(r2)  # 输出 https://www.baidu.com/
```
