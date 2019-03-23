---
export_on_save:
  html: true
html:
  toc: true
  offline: true
toc:
  depth_from: 1
  depth_to: 3
  ordered: false

---
# 欢迎来到我的笔记

笔记尚待完善，陆续会有项目专题。
[我的仓库](https://github.com/JK-97)

---
# 1.python语言


## 1.1.python语言特点
**动态语言**
* 编译器还是运行期确定类型
* python是在运行期确定类型的

**强类型**
* 会不会发生隐式转换
* python是强类型语言

**优缺点**
* 胶水语言，轮子多，应用广泛
* 语言灵活，生产力高
* 性能问题，代码维护，python2/3差异

**拥有自省功能**
* 在运行时能够获得对象的类型
* type()，判断对象类型
* dir()， 带参数时获得该对象的所有属性和方法；不带参数时，返回当前范围内的变量、方法和定义的类型列表
* isinstance()，判断对象是否是已知类型
* hasattr()，判断对象是否包含对应属性
* getattr()，获取对象属性
* setattr()， 设置对象属性

**猴子补丁**
* 猴子补丁是程序在本地扩展或修改支持系统软件的方式（仅影响程序的运行实例）
* 所谓mankey patch 就是运行时替换
* 比如gevent库需要修改内置的socket
* from gevent import monkey；
monkey.patch_socket()
将阻塞soket替换成非阻塞socket

**鸭子类型**
* 如果里看到一个鸟，走起来像鸭子，叫起来像鸭子，那么它就是鸭子
* 更关注接口
---
## 1.2.python2/3差异
**不同**
* print成为了函数
* 不再有Unicode，默认str就是nuicode
* 除法，除号返回浮点数
* 优化super函数
```python
    retru super(C,self).func()#py2
    return super().func()#py3
```
* keyword only argument限定关键字参数
```python
def add(a,b,*,c):
    pass
def add(**kwargs):
    pass
```
* 高级解包操作，a,b，*rest = range(10) 
* 类型注解：type hint:def hello(name:str) ->str:
* chaied exception， py3重新抛出异常不会丢失栈信息
* 一切返回迭代器 range,zip,map,dict,values,etc,are all iterators

**新增**
* yeld from 连接
* asyncio，async/wait 原生协程支持异步编程
* 新增enum，mock，asyncio，ipaddress，concurrent.futures
* 生成的pyc文件统一放到__pycache__
* 内置库修改，urllib，selector

**兼容2/3的代码**
* six
* 2to3等工具转换代码格式
* \_\_future__

**可变/不可变对象**
* 不可变对象：bool/int/float/tuple/str/frozenset
* 可变对象：list/set/dict 




---
# 2.算法与数据结构

## 2.1.排序算法
**快速排序算法**

```python {.line-numbers}
def quicksort(array):
    if len(array) < 2:
        return array
    else:
        pivot_index = 0  #第一个元素作为主元
        pivot = array[pivot_index]
        less_part = [i for i in array[pivot_index + 1:] if i <= pivot]
        great_part = [i for i in array[pivot_index + 1:] if i > pivot]
        return quicksort(less_part) + [pivot] + quicksort(great_part)
def test_quicksort():
    import random
    l1 = [range(10)]
    random.shuffle(l1)
    assert quicksort(l1) == sorted(l1)


test_quicksort()
```
---
**归并排序算法算法**
```python {.line-numbers}

def merge_sorted_seq(sorted_a, sorted_b):
    length_a, length_b = len(sorted_a), len(sorted_b)
    a = b = 0
    new_sorted_seq = []
    while a < length_a and b < length_b:
        if sorted_a[a] < sorted_b[b]:
            new_sorted_seq.append(sorted_a[a])
            a += 1
        else:
            new_sorted_seq.append(sorted_b[b])
            b += 1
    if a < length_a:
        new_sorted_seq.extend(sorted_a[a:])
    else:
        new_sorted_seq.extend(sorted_b[b:])
    return new_sorted_seq


def test_merge_sorted_seq():
    a = [1, 2, 5]
    b = [0, 3, 4, 8]
    print(merge_sorted_seq(a, b))


def merge_sort(array):
    if len(array) <= 1:
        return array
    else:
        mid = int(len(array) / 2)
        left_array = merge_sort(array[:mid])
        right_array = merge_sort(array[mid:])
        return merge_sorted_seq(left_array, right_array)


def test_merge_sort():
    import random
    l1 = list(range(10))
    random.shuffle(l1)
    assert merge_sort(l1) == sorted(l1)


test_merge_sort()
```
---
## 2.2.数据结构

**链表**
```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        pre =None
        cur = head
        while cur:
            nextnode = cur.next
            cur.next = pre
            pre = cur 
            cur = nextnode
        return pre

```
**队列**
```python
from collections import deque


class Queue:
    def __init__(self):
        self.item = deque()

    def append(self, val):
        return self.item.append(val)

    def pop(self):
        return self.item.popleft()

    def empty(self):
        return len(self.item) == 0

```
**栈**

```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack=[]

    def push(self, x: int) -> None:
        self.stack.append(x)
    def pop(self) -> None:
        self.stack.pop()
        
    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return min(self.stack)


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```


**树**
```python

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        stack = []
        if root is not None:
            stack.append((1, root))
        
        depth = 0
        while stack != []:
            current_depth, root = stack.pop()
            if root is not None:
                depth = max(depth, current_depth)
                stack.append((current_depth + 1, root.left))
                stack.append((current_depth + 1, root.right))
        
        return depth
```
# 3.编程范式
## 3.1.装饰器
**函数装饰器**
```python
import time


def log_time(func):
    def _log(*args, **kwargs):
        beg = time.time()
        res = func(*args, **kwargs)
        print('use time: {}'.format(time.time() - beg))
        return res

    return _log


@log_time
def mysleep():
    time.sleep(1)


mysleep()
```
**类装饰器**
```python
import time

class LogTime:
     def __call__(self,func):
        def _log(*args, **kwargs):
            beg = time.time()
            res = func(*args, **kwargs)
            print('use time: {}'.format(time.time() - beg))
            return res

        return _log


@LogTime()
def mysleep():
    time.sleep(1)


mysleep()
```

## 3.2.面向对象
**概念**
* 把对象作为基本单元，把对象抽象成类
* 数据封装，继承，多态

**举个例子：**
```python
class person(object): #py3可以直接class person
    def __init__(self,name,age):
        self.name = name
        self.age = age
    
    def print_name(self):
        print("my name is {}".format(self.name))
```
&emsp;&emsp;方法中我们可以看到方法的参数中都带有self这个关键字，这么的意义是指，这些方法都只能通过类创建的对象调用，self代表对象自己。我们称之为”方法“。而那些如self.attr_name的，我们成为实例属性
**组合与继承**
* 组合是使用其他的类实例作为自己的一个属性(Has-a关系)
* 子类继承父类的属性和方法(Is-a)
* 优先使用组合保持代码简单

**类变量和实例变量**
* 类变量由所有实例共享
* 实例变量单独享有，不同实例之间不影响
* 当我们需要在一个类的不同实例之间共享变量的时候使用类变量

**方法装饰器**
* 都可以通过Class.method()的方式使用
* classmethod第一个参数是cls，可以引用类变量
* staticmethod使用起来和普通函数，只不过放在类里去组织

**元类**

***元类是创建类的类***
* 元类允许我们控制类的生成，比如修改类的属性
* 使用type来定义原类
* 元类最常见的一个使用场景就是ORM框架
```python
#观看文档这两种定义是等价的。
>>> class X:
...     a = 1
...
>>> X = type('X', (object,), dict(a=1))
```

```python
class Base:
    pass

class Child(Base):
    pass

#等价定义注意Base后要加逗号否证就不是tuple了
SameChild = type('Child',(Base,)m|{})
#此操作与上无区别

#加上方法
class ChildWithMethod(Base):
    bar = True

    def hello(self):
        print('hello')
def hello():
    print('hello')

type('ChildWithMethod',(Base,),{'bar':Ture,'hello':hello})
```

---
# 4.网络协议


## 4.1.基本概念
**协议表**
![protal ](https://jk-97.github.io/my_note/sources/dasdgnhy.png)
**浏览器输入一个url中间经历的过程**
![request](https://jk-97.github.io/my_note/sources/1061765-20161211174151304-1668168182.png)
**TCP三次握手**
![tcp 3 times ](https://jk-97.github.io/my_note/sources/1061765-20161211174151304-1668168182.png)
**TCP四次挥手**
![tcp 4 times ](https://jk-97.github.io/my_note/sources/1061765-20161211181122866-333961282.png)
[reference：https://www.cnblogs.com/huangjianping/p/7998067.html==](https://www.cnblogs.com/huangjianping/p/7998067.html)

## 4.2.HTTP协议
 &emsp;&emsp;在Web应用中，服务器把网页传给浏览器，实际上就是把网页的HTML代码发送给浏览器，让浏览器显示出来。而浏览器和服务器之间的传输协议是HTTP，所以：

 * 是一种用来定义网页的文本，会HTML，就可以编写网页；
 * 是在网络上传输HTML的协议，用于浏览器和服务器的通信。
>
> ***步骤1***：浏览器首先向服务器发送HTTP请求，请求包括：
> 方法：GET还是POST，GET仅请求资源，POST会附带用户数据；
> 路径：/full/url/path；
> 域名：由Host头指定：Host: www.sina.com.cn
> 以及其他相关的Header；
> 如果是POST，那么请求还包括一个Body，包含用户数据。
> 
> ***步骤2***：服务器向浏览器返回HTTP响应，响应包括：
> 响应代码：200表示成功，3xx表示重定向，4xx表示客户端发送的请求有错误，5xx表示服务器端处理时发生了错误；
> 响应类型：由Content-Type指定；
> 以及其他相关的Header；
> 通常服务器的HTTP响应会携带内容，也就是有一个Body，包含响应的内容，网页的HTML源码就在Body中。
> 
> ***步骤3***：如果浏览器还需要继续向服务器请求其他资源，比如图片，就再次发出HTTP请求，重复步骤1、2。
> Web采用的HTTP协议采用了非常简单的请求-响应模式，从而大大简化了开发。当我们编写一个页面时，我们只需要在HTTP请求中把HTML发送出去，不需要考虑如何附带图片、视频等，浏览器如果需要请求图片和视频，它会发送另一个HTTP请求，因此，一个HTTP请求只处理一个资源。

**什么是长链接？**
* 短链接： 连接请求——数据传输——断开连接
* 长连接： 保持一段时间不断开tcp连接
* 告诉他长度 conten—length

**cookies和sesion区别**
* Session 一般是服务器生成后给客户端
* Cookie 是实现session的一种机制，通过HTTP cookie字段实现
* Session 通过在服务器保存sessionid 识别用户，cookie 存储在客户端
---
# 5.Linux相关

## 5.1.Linux储备
**常考察方向**
* 在Linux服务器上操作
* 了解Linux工作原理和常用工具
* 需要了解查看文件，进程，内存相关的一些命令，用来调试

**如何查询linux命令用法**
* 使用man命令查询用法。但是man手册比较晦涩
* 工具自带dehelp
* man的替代品tldr

**文件/目录操作命令**
* chown/chmode/chgrp
* ls/rm/cd/mv/touch/rename/ln(软链接和硬链接)等
* locate/find/grep定位查找搜索

**文件查看**
* 编辑器vi/nano
* cat/head/tail查看文件
* more/less交互式查看文件

**进程操作命令**
* ps查看进程
* kill杀死进程
* top/htop监控进程

**内存操作命令**
* free查看可用内存
* 了解每一列的具体含义
* 排查内存泄漏问题

**网络操作命令**
* ifconfig查看网卡信息
* lsof/netstat查看端口信息
* ssh/scp远程登录复制
* tcpdump抓包

**用户/组操作命令**
* useradd/usermod
* groupadd/groundmod
---


## 5.2.操作系统内存管理机制

**什么是分页机制**
操作系统为了搞笑管理内存，减少碎片，逻辑地址和物理地址分离的内存分配管理方案
* 程序的逻辑地址划分为固定大小的页(Page)
* 物理地址划分为同样大小的帧(Frame)
* 通过页表对应逻辑地址和物理地址
> ![分页](https://jk-97.github.io/my_note/sources/asdsadsd.png)

**什么是分段机制**
分段式为了满足代码的一些逻辑需求
* 数据共享，数据保护，动态链接库等
* 通过段表实现逻辑地址和物理地址的映射关系
* 每个段类不式连续内存分配，段和段直接式离散分配的(每个段是出于实现相同的一个功能来进行分配)
> ![分段](https://jk-97.github.io/my_note/sources/dsadsafa.png)

**分页和分段的区别**
* 页是出于内存利用率的角度提出离散分配机制
* 段是出于用户角度，出于用户数据保护，数据隔离等用途的管理机制
* 页的大小是固定的，操作系统决定；段的大小不确定，用户程序决定

**什么是虚拟内存**
通过把一部分了暂时不用的的内存信息放到硬盘上
* 局部性原理，程序运行时候只有部分必要的信息转入内存
* 内存中暂时不需要的内容放到硬盘上
* 系统似乎提供了比实际内存大得很多的内存容量，称之为虚拟内存

**什么是内存抖动**
* 本质是频繁的页调度行为
* 频繁的页调度，进程不断产生缺页中断
* 置换一个页，又不断再次需要这个页
* 运行程序太多；分页替换策略不好。终止进程或者增加物理内存

**Python的垃圾回收机制原理**
* 引用计数为主(缺点：循环引用无法解决)
* 引用标记清楚和分代回收解决引用计数的问题
* 引用计数为主+标记清除和分代回收为辅

**引用计数**
```python
a = [1]     #ref 1
b = a       #ref 2
b=None      #ref 1  
del a       #ref 0  回收
```
**标记清除**
```python
a = [1]     #a ref 1 
b = [2]     #b ref 1
a.append(b) #b ref 2
b.append(a) #a ref 2
del a       #a ref 1
del b       #b ref 1    无法归零回收
```
> ![标记清楚](https://jk-97.github.io/my_note/sources/dsadas.png)
> 通过root节点搜索可以达到的节点，不可达到的点标为灰色，回收

***分代回收***
* 给对象记录下一个age，随着每一次垃圾回收，这个age会增加；
* 给不同age的对象分配不同的堆内内存空间，称为某一代；
* 对某一代的空间，有适合其的垃圾回收算法；
* 对每代进行不同垃圾回收，一般会需要一个额外的信息：即每代中对象被其他代中对象引用的信息。这个引用信息对于当前代来说，扮演与"root"一样的角色，也是本代垃圾回收的起点。

## 5.3.操作系统线程和进程常考题
**进程和线程对比**
* 进程是对运行时程序的封装，时系统资源调度的基本单位
* 线程是进程的子任务，cpu调度和分配的基本单位，实现进程内并发，并行
    * 并行是真正的多核运行
    * python由于GIL不能真正的并行，看似并发
* 一个进程都可以包含多个线程，线程依赖进程存在，并共享进程内存

**什么是线程安全**
* 一个操作可以再多线程环境中安全使用，获取正确的结果
* 线程安全的操作好比线程是顺序执行而不是并发执行的(i+=1)
* 一般如果涉及到写操作需要考虑如何让多个线程安全访问数据

**线程同步方式**
* 互踩量：通过互斥机制防止多个线程同时访问公共资源
* 信号量(Semphare):threading.Semphare(valuse = 1)控制同一时刻多个线程访问同一个资源的线程数
* 事件(信号)：通过通知的方式保持多个线程同步

**进程间通信的方式(IPC)**
* 管道/匿名管道/有名管道(pipe)
* 信号(Signal):比如用户使用Ctrl+c产生SIGINT程序终止信号
* 消息队列(Message)
* 共享内存(share memory)
* 信号量(Semaphore)
* 套接字(socket):最常用的方式，我们的web应用都是这种方式

**Python使用多线程**(python开发适用于I/O密集型的应用)
* threading.Thread类来创建线程
* start()方法启动进程
* 可以用join()等待线程结束

**Python使用多进程程**(python开发使用于计算密集型的应用)
* mltiprocessing多进程模块
* Multiprocessing.Process类实现对进程
* 避免GIL的影响
---

# 6.数据库

## 6.1.数据库种类
**如图:**
> ![database ](https://jk-97.github.io/my_note/sources/228680-448d468546343fa9.png)
> 
**关系型数据库介绍**
 

1. ***关系型数据库的由来***
    &emsp;&emsp;虽然网状数据库和层次数据库已经很好的解决了数据的集中和共享问题，但是在数据库独立性和抽象级别上扔有很大欠缺。用户在对这两种数据库进行存取时，仍然需要明确数据的存储结构，指出存取路径。而关系型数据库就可以较好的解决这些问题。

2. ***关系型数据库介绍***
    &emsp;&emsp;关系型数据库模型是把复杂的数据结构归结为简单的二元关系（即二维表格形式）。在关系型数据库中，对数据的操作几乎全部建立在一个或多个关系表格上，通过对这些关联的表格分类、合并、连接或选取等运算来实现数据库的管理。

    &emsp;&emsp;关系型数据库诞生40多年了，从理论产生发展到现实产品，例如：Oracle和MySQL，Oracle在数据库领域上升到霸主地位，形成每年高达数百亿美元的庞大产业市场。

3. **关系型数据库表格之间的关系举例**
![table ](https://jk-97.github.io/my_note/sources/228680-945f5401f695df78.png)
 

**非关系型数据库介绍**
 

1. ***非关系型数据库诞生背景***
    &emsp;&emsp;NoSQL，泛指非关系型的数据库。随着互联网web2.0网站的兴起，传统的关系数据库在应付web2.0网站，特别是超大规模和高并发的SNS类型的web2.0纯动态网站已经显得力不从心，暴露了很多难以克服的问题，而非关系型的数据库则由于其本身的特点得到了非常迅速的发展。NoSql数据库在特定的场景下可以发挥出难以想象的高效率和高性能，它是作为对传统关系型数据库的一个有效的补充。

    &emsp;&emsp;NoSQL(NoSQL = Not Only SQL )，意即“不仅仅是SQL”，是一项全新的数据库革命性运动，早期就有人提出，发展至2009年趋势越发高涨。NoSQL的拥护者们提倡运用非关系型的数据存储，相对于铺天盖地的关系型数据库运用，这一概念无疑是一种全新的思维的注入。

2. ***非关系型数据库种类***

    （1）键值存储数据库（key-value）
    &emsp;&emsp;键值数据库就类似传统语言中使用的哈希表。可以通过key来添加、查询或者删除数据库，因为使用key主键访问，所以会获得很高的性能及扩展性。
    键值数据库主要使用一个哈希表，这个表中有一个特定的键和一个指针指向特定的数据。Key/value模型对于IT系统来说的优势在于简单、易部署、高并发。
    典型产品：Memcached、Redis、MemcacheDB

    （2）列存储（Column-oriented）数据库
    &emsp;&emsp;列存储数据库将数据存储在列族中，一个列族存储经常被一起查询的相关数据，比如人类，我们经常会查询某个人的姓名和年龄，而不是薪资。这种情况下姓名和年龄会被放到一个列族中，薪资会被放到另一个列族中。

    这种数据库通常用来应对分布式存储海量数据。

    典型产品：Cassandra、HBase

    （3）面向文档（Document-Oriented）数据库

    &emsp;&emsp;文档型数据库的灵感是来自于Lotus Notes办公软件，而且它同第一种键值数据库类似。该类型的数据模型是版本化的文档，半结构化的文档以特定的格式存储，比如JSON。文档型数据库可以看作是键值数据库的升级版，允许之间嵌套键值。而且文档型数据库比键值数据库的查询效率更高。

    &emsp;&emsp;面向文档数据库会将数据以文档形式存储。每个文档都是自包含的数据单元，是一系列数据项的集合。每个数据项都有一个名词与对应值，值既可以是简单的数据类型，如字符串、数字和日期等；也可以是复杂的类型，如有序列表和关联对象。数据存储的最小单位是文档，同一个表中存储的文档属性可以是不同的，数据可以使用XML、JSON或JSONB等多种形式存储。

    典型产品：MongoDB、CouchDB

    （4）图形数据库

    &emsp;&emsp;图形数据库允许我们将数据以图的方式存储。实体会被作为顶点，而实体之间的关系则会被作为边。比如我们有三个实体，Steve Jobs、Apple和Next，则会有两个“Founded by”的边将Apple和Next连接到Steve Jobs。

    典型产品：Neo4J、InforGrid


> [reference：https://blog.csdn.net/qq_27565769/article/details/80731213 ](https://blog.csdn.net/qq_27565769/article/details/80731213 )

---

## 6.2.MYSQL
### 6.2.1.MYSQL概念
**常考察点**
* 事务原理，特性，事务的并发控制
* 常用字段，含义，区别
* 常用数据库引擎的区别

**事务 Transaction**
* 事务是数据库并发控制的基本单位
* 事务可以看作是一系列SQL语句的集合
* 事务必须要么全部执行成功，要么全部执行失败

**特性ACID**
* 原子性(Atomicity)：一个事务所有操作全部完成或失败
* 一致性(Consistency):事务开始和结束后数据的完整性没有被破坏
* 隔离性(Isolation):允许多个事务同时对数据库修改和读写
* 持久性(Durability)：事务结束后，修改时永久不会丢失的

**事务的并发可能会产生的四种异常情况**
* 幻读(phanton read):一个事务第二次查出第一次没有的结果
* 非重复读(nonrepeatable read): 一个事务重复读两次得到不同结果
* 脏读(dirty read):一个事务读取到另外一个事务没有提交的修改
* 丢失修改(lost update):并发写入造成其中一些修改丢失

**四种事务隔离级别**
* 读取提交(read uncommitted):别的事务可以读取到未提交改变
* 读已提交(read committed):只能读取已提交的数据
* 可重复读(repeatable read):同一个事务先后查询结果一样(Mysql InoDB默认实现可重复读级别)
* 串行化(Serialzavle)：事务串行化的执行，隔离级别最高，执行效率最低

**如何解决并发场景下的插入重复**
* 使用数据库的唯一索引(一般情况用不了，一般项目会建库建表)
* 使用队列异步写入
* 使用redis等实现分布式锁

**乐观锁和悲观锁**
* 悲观锁是先获取在进行操作。一锁二查三更新select for update
* 乐观锁先修改，更新的时候发现数据已经变了就回滚(测check and set)
* 根据响应速度，冲突频率，重试代价来判断选择哪种

**MYSQL数据类型**
1. 字符串
    CHAR:存储定长字符串
    VARCHAR：存储不定长字符串
    TEXT:存储较长的文章
2. 数值
    TINTINT,INT,BIGINT,DOUBLE等
3. 日期和时间
    DATE：YYYY-MM-DD
    DATETIME:YYYY-MM-DD HH:MM:SS

**Mysql常用引擎**
* MyISAM不支持事务，InnoDB支持事务
* MyISAM不支持外键，InnoDB支持外键
* MyISAM只支持表锁，InnoDB支持表锁和行锁


### 6.2.1.索引原理以及优化
* 索引的原理，类型，结构
* 创建索引的注意事项，使用原则
* 创建排查和消除慢查询

**什么是索引?**
* 索引是数据表中一个或多个列进行排序的数据结构
* 索引能够大幅度提升检索速度(回顾下查找结构：二叉搜索树，平衡数，多路平衡数)
* 创建，更新索引本身也会消耗空间和时间

**查找结构进化史**
* 线性查找：一个一个找，实现简单，速度慢
* 二分查找：简单，查找快，但要求是有序的，插入特别慢
* HASH：查询快，占用空间，不太适合存储大规模的数据
* 二叉查找树：插入和查询很快(log(n))，无法存大规模数据，复杂退化问题
* 平衡数：解决bst退化的问题，树是平衡的；节点非常多的时候，树依然很高
* 多路查找树：一个父亲多个孩子节点，书不会特别深
* 多路平衡查找树：B-Tree

> [数据结构可视化网站](https://：www.cs.usfca.edu/~galles/visualization/Algorithms.html)

**什么是B-Tree?**
* 多路平衡查找树(每个节点最多m(m>=2)个孩子，称为m阶或者度)
* 叶节点具有相同深度
* 节点中的数据key从做到右四递增的

**什么是B+Tree**
* Mysql实际使用的是B+Tree作为索引的数据结构
* 只在叶子节点带有指向的指针，可以增加书的度
* 叶子节点通过指针相连，实现范围查询

**Mysql索引类型**
* 普通索引
* 唯一索引
* 多列索引
* 主键索引
* 全文索引InnoDB不支持

**什么时候创建索引**
* 经常用作查询条件的字段(WHERE条件)
* 经常用锁表连接的字段
* 经常出现order by，ground by之后的字段

**创建索引右那些需要注意的**
* 非空字典NOT NULL，Mysql很难多空值查询优化
* 区分度高，离散度大，作为索引的字段值尽量不要右大量相同值
* 索引长度不要太长(比较耗费时间)

**索引什么时候失效**
* 模糊匹配：以%开头的LIKE语句，模糊搜索
* 类型隐转：出现隐式类型转换(在python这种动态语言中查询需要特别注意)
* 没有满足最左前缀原则

**什么式聚集索引和非聚集索引**
* 聚集还是非聚集指的式B+Tree叶节点的是指针还是数据记录
* MyISAM索引和数据分离，使用的是非聚集索引
* InnoDB数据文件就是索引文件，主键索引就是聚集索引

**如何排查慢查询**
* 慢查询通常是缺少索引，索引不合理或业务逻辑代码实现导致
* slow_query_log_file开启并且查询了慢查询日志
* 通过explain排查索引问题
* 调整数据修改索引；业务代码层限制不合理访问
----
### 6.2.2.Mysql语句常考题
**SQL语句已考察各种各种连接为重点**
* 内链接(INNER JOIN)：两个表存在匹配时，才会返回匹配行
    * 将左表和右表能关联起来的数据连接后返回
    * 类似于求两个表的“交集”
    * select * from A innner join B on a .id =v .id
* 外连接(LEFT/RIGHT JOIN)：返回一个表的行，即使另外一个没有匹配
    * 左连接返回坐标中所有记录，几时右表中没有匹配的记录
    * 左连接返回右表中所有记录，几时坐标中没有匹配的记录
    * 没有匹配的字段会设置成NULL
    * Mysql中使用left join和right jion实现
* 全链接(FULL  JOIN):只要某一个表存在匹配就返回
    * 只要某一个表存在匹配，就返回行
    * 类似求两个表的“并集”
    * 但是Mysql不支持，可以用left jion，union，right join联合使用模拟
### 6.2.3.Mysql思考题
* 为什么Mysql数据库的主键使用自增的增数比较好？
&emsp;&emsp;对于这个问题需要从MySQL的索引以及存储引擎谈起：
&emsp;&emsp;InnoDB的primary key为cluster index,除此之外，不能通过其他方式指定cluster index,如果InnoDB不指定primary key,InnoDB会找一个unique not null的field做cluster index,如果还没有这样的字段，则InnoDB会建一个非可见的系统默认的主键---row_id(6个字节长)作为cluster_index。
&emsp;&emsp;建议使用数字型auto_increment的字段作为cluster index。不推荐用字符串字段做cluster index (primary key) ,因为字符串往往都较长， 会导致secondary index过大(secondary index的叶子节点存储了primary key的值),而且字符串往往是乱序。cluster index乱序插入容易造成插入和查询的效率低下。

* 使用uuid可以？为什么？
    * 自增ID节省一半磁盘空间
    * 单个数据走索引查询，自增id和uuid相差不大
    * 范围like查询，自增ID性能优于UUID
    * 写入测试，自增ID是UUID的4倍
    * 备份和恢复，自增ID性能优于UUID
* 如果是分布式系统下怎么生成数据库的自增
分布式架构，意味着需要多个实例中保持一个表的主键的唯一性。这个时候普通的单表自增ID主键就不太合适，因为多个mysql实例上会遇到主键全局唯一性问题。
    * 自增ID主键+步长，适合中等规模的分布式景
&emsp;&emsp;在每个集群节点组的master上面，设置（auto_increment_increment），让目前每个集群的起始点错开 1，步长选择大于将来基本不可能达到的切分集群数，达到将 ID 相对分段的效果来满足全局唯一的效果。
&emsp;&emsp;优点是：实现简单，后期维护简单，对应用透明。
 &emsp;&emsp;缺点是：第一次设置相对较为复杂，因为要针对未来业务的发展而计算好足够的步长;
    * UUID，适合小规模的分布式环境
&emsp;&emsp;对于InnoDB这种聚集主键类型的引擎来说，数据会按照主键进行排序，由于UUID的无序性，InnoDB会产生巨大的IO压力，而且由于索引和数据存储在一起，字符串做主键会造成存储空间增大一倍。
&emsp;&emsp;在存储和检索的时候，innodb会对主键进行物理排序，这对auto_increment_int是个好消息，因为后一次插入的主键位置总是在最后。但是对uuid来说，这却是个坏消息，因为uuid是杂乱无章的，每次插入的主键位置是不确定的，可能在开头，也可能在中间，在进行主键物理排序的时候，势必会造成大量的 IO操作影响效率，在数据量不停增长的时候，特别是数据量上了千万记录的时候，读写性能下降的非常厉害。
优点：搭建比较简单，不需要为主键唯一性的处理。
缺点：占用两倍的存储空间（在云上光存储一块就要多花2倍的钱），后期读写性能下降厉害。
    * 雪花算法自造全局自增ID，适合大数据环境的分布式场景。由twitter公布的开源的分布式id算法snowflake
---
## 6.3.Redis
### 6.3.1.Redis概念
* 为什么使用缓存？使用场景？
    * 常用的内存缓存有Redis和Memcached
    * 缓存关系数据库并访问的压力：热点数据
    * 减少响应时间：内存IO速度必磁盘快
    * 提升吞吐量：Redis等内存数据库单机可以支撑很大并发
![redis与memcached](https://jk-97.github.io/my_note/sources/1552619755.png)
* Redis的常用数据类型，使用方式
    * Sring:用来实现简单的KV键值对，比如计数器
    * List：实现双向链表，比如用户的关注，粉丝列表
    * Hash：用来存储彼此相关的键值对，HSET key filed value
    * Set：存储不重复元素，比如用户的关注者
    * Sorted Set：实时信息排行榜
* Redis内置实现
    * C语言底层实现
    * String：整数或者sds(Simple Dynamic String)
    * List：ziplist或者double linked list
    * Hash：ziplist或者hashtable
    * Set：intset或者hashtable
    * SortedSet:skiplist 跳跃表
* Redis有哪些持久化方式？
    * 快照方式：把数据快照放在磁盘二进制文件中，dump.rdb，指定时间间隔把Redis数据库状态保存到一个压缩的二进制文件中，缺点：若宕机，间隔内的数据全部丢失
    * AOF(Append Only File)：每一个写命令保存到appendonly.aof中。缺点，虽然不会丢失大量数据，但文件比较大，恢复速度比较慢
* Redis事务
    * 将多个请求打包，一次性，按序执行多个命令的机制
    * Rdis通过MULTI,EXEC,WATCH等命令实现事务功能
    * Python redis-py pipeline = conn.pipeline(transaction =True)
* Redis如何实现分布式锁
    * 使用setnx实现加锁，可以同时通过expire添加超时时间
    * 锁的valuse值可以使用一个随机的uuid或者待定的命名
    * 释放锁的时候，通过uuid判断是否是该锁，是则执行delete释放锁
    [Redis分布式锁的实现原理看这篇就够了](https://blog.csdn.net/gupao123456/article/details/84327254)
* 使用缓存的模式？
    * Cache Aside：同时更新缓存和数据库(先更新数据库后更新缓存，并发写操作可能导致缓存读取的是脏数据，一般先更新数据库然后删除缓存，下次读取时再重建缓存)
    * Read/Write Throught：先更新缓存，缓存负责同步更新数据库
    * Write Behind Caching：先更新缓存，缓存顶起异步更新数据库
* 缓存使用问题：数据一致性问题；缓存穿透，击穿，雪崩
    * 缓存穿透：大量查询不到的数据请求落到后端数据库，数据库压力增大(很多无脑爬虫通过自增id的方式爬取网站，网站查不到相关id的数据)
        * 原因：由于大量缓存查不到就去数据库取，数据库也没有要差的数据
        * 解决：对于没查到返回为None的数据也缓存
        * 插入数据的时候删除相应缓存，或者设置较短的超时时间
    * 缓存击穿：某些非常热点的数据key过期，大量请求打到后端数据库
        * 原因：热点数据key失效导致大量请求打到数据库增加数据库压力
        * 解决：分布式锁：获取锁的线程从数据库拿去数据更新缓存，其他线程等待。异步后台更新：后代任务针对过期的key自动刷新
    * 缓存雪崩：缓存不可用或者大量缓存key同时失效，大量请求直接打到数据库
        * 解决：多级缓存：不同级别的key设置不同的超时时间。随机超时：key的超时时间随机设置，防止同时超时。架构层：提升系统可用性，监控，报警完善

---

### 6.3.2.Redis分布式锁应用
* 请里基于redis编写实现一个简单的分布式锁(要求支持超时参数)
* 如果Redis单个节点宕机了，如何处理？还有其他业界的方案实现分布式锁么？

---
# 7.爬虫
## 7.1.技术储备
### 7.1.1.开发环境
* pycharm 
* mysql+redis+etri

**技术选型**
* scrapy vs requests + beatifulsoup
* request 和beatifulsoup都是库，scrapy是框架
* scrapy框架加入
* scrapy基于twsted，性能最大的优势
* scrapy方便拓展，提供了很对内置的功能
* scrapy内置的css和xpath selector非常方便，beautifulsoup最大的缺点就是慢

**网页分类**
* 静态网页
* 动态网页
* webservice(restapi)

### 7.1.2.正则表达式
字符 | 描述
------------ | -------------
\cx	|匹配由x指明的控制字符。例如， \cM 匹配一个 Control-M 或回车符。x 的值必须为 A-Z 或 a-z 之一。否则，将 c 视为一个原义的 'c' 字符。
\f	|匹配一个换页符。等价于 \x0c 和 \cL。
\n	|匹配一个换行符。等价于 \x0a 和 \cJ。
\r	|匹配一个回车符。等价于 \x0d 和 \cM。
\s	|匹配任何空白字符，包括空格、制表符、换页符等等。等价于 [ \f\n\r\t\v]。注意 Unicode 正则表达式会匹配全角空格符。
\S	|匹配任何非空白字符。等价于 [^ \f\n\r\t\v]。
\t	|匹配一个制表符。等价于 \x09 和 \cI。
\v	|匹配一个垂直制表符。等价于 \x0b 和 \cK。

---
字符|描述
------------- | -------------
$  | 匹配输入字符串的结尾位置。如果设置了 RegExp 对象的 Multiline 属性，则 \$ 也匹配 '\n' 或 '\r'。要匹配 $ 字符本身，请使用 \$。
( )	|标记一个子表达式的开始和结束位置。子表达式可以获取供以后使用。要匹配这些字符，请使用 \( 和 \)。
*	|匹配前面的子表达式零次或多次。要匹配 * 字符，请使用 \*。
+	|匹配前面的子表达式一次或多次。要匹配 + 字符，请使用 \+。
.	|匹配除换行符 \n 之外的任何单字符。要匹配 . ，请使用 \. 。
[	|标记一个中括号表达式的开始。要匹配 [，请使用 \[。
?	|匹配前面的子表达式零次或一次，或指明一个非贪婪限定符。要匹配 ? 字符，请使用 \?。
\	|将下一个字符标记为或特殊字符、或原义字符、或向后引用、或八进制转义符。例如， 'n' 匹配字符 'n'。'\n' 匹配换行符。序列 '\\' 匹配 "\"，而 '\(' 则匹配 "("。
^	|匹配输入字符串的开始位置，除非在方括号表达式中使用，此时它表示不接受该字符集合。要匹配 ^ 字符本身，请使用 \^。
{	|标记限定符表达式的开始。要匹配 {，请使用 \{。
\|	|指明两项之间的一个选择。要匹配 |，请使用 \|。

---
字符|描述
------------- | -------------
*	| 匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。
+	|匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
?	|匹配前面的子表达式零次或一次。例如，"do(es)?" 可以匹配 "do" 、 "does" 中的 "does" 、 "doxy" 中的 "do" 。? 等价于 {0,1}。
{n}	|n 是一个非负整数。匹配确定的 n 次。例如，'o{2}' 不能匹配 "Bob" 中的 'o'，但是能匹配 "food" 中的两个 o。
{n,}	|n 是一个非负整数。至少匹配n 次。例如，'o{2,}' 不能匹配 "Bob" 中的 'o'，但能匹配 "foooood" 中的所有 o。'o{1,}' 等价于 'o+'。'o{0,}' 则等价于 'o*'。
{n,m}	|m 和 n 均为非负整数，其中n <= m。最少匹配 n 次且最多匹配 m 次。例如，"o{1,3}" 将匹配 "fooooood" 中的前三个 o。'o{0,1}' 等价于 'o?'。请注意在逗号和两个数之间不能有空格。

---



# 8.框架语言


## 8.1.什么是WSGI
* python web server gateway interface
* 解决了python webserver乱象 mode——python，CGI。fastCGI
* 描述了web server 如何与web框架交互，web框架如何请求处理

```python
#一个简单的wsgi应用
def myapp(environ, start_resopnce):
    status = '200 OK'
    header = [('Conten-Typr', 'text/html;charset=utf-8')
              ]
    start_resopnce(status, header)
    return [b'<h1>Hello world</h1>']


if __name__ == "__main__":
    from wsgiref.simple_server import make_server
    httpd = make_server('127.0.0.1', 8888, myapp)
    httpd.serve_forever()


```

## 8.2.常用pythonweb框架

## 8.3.web框架组成
MVC

## 8.4.RESTful
* 前后端分离的意义和方式
* 什么是RESTful
* 如何设计RESTful API

前后端解耦，接口复用，减少开发量
各司其职，前后端同步开发，提升工作效率，定义好接口规范
更有利于调试(mock)测试和运维部署

**representtational state transfer**
表现层状态转移，由HTTP协议的主要设计者RoyFielding提出
资源(resources)，表现层(representation)，状态转化(statr transfer)
是一种以资源为为中心的web软件架构风格，可以用ajax和resful web服务构建应用
* resources：使用url指向一个实体
* representation：资源的表现形式，比如图片，HTML文本等
* statr transfer状态转化：get，post，putdelete http动词来操作资源，实现资源的改变

**resful的准则**
所有思维u抽象围殴至于那，资源对应唯一的标识
资源通过接口进行操作实现状态转移，操作本身无状态
对之u按的操作不会改变资源的标识

**restful api**
通过get，post，put delete http 获取/新疆/更新/删除
一般使用json格式返回数据
一般web框架都有相应的插件支持resfulapi

**什么是https**
* https和http的区别是什么
* 什么是对称加密和非对称加密 

---




