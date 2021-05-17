---
title: 数据科学笔记（一）：narray基本操作
date: 2021-05-17 23:13:07
tags:
  - 数据科学
  - python
  - numpy
  - 笔记
categories:
  - 技术力小本本
---
### 数据处理的一般流程

#### 数据收集

1.网络爬虫

2.公开数据集

3.其他途径收集的数据

#### 数据预处理

方法：归一化、二值化、维度变换、去重、无效数据过滤

#### 数据处理

1.数据排序

2.数据查找

3.数据统计分析（mainly)

#### 数据展示

1.列表

2.图标

3.动态交互图形（可以与前端相连接）



### Numpy 基础

处理大量数据时，numpy 处理速度比py 更快，效率更高

导入numpy后创建数组：

py中直接

~~~python
data = [1，2，3，4，5]
~~~

即可。

np中需要 

~~~python
data = np.array([1,2,3,4,5])
~~~

才能创建数组。

以上为一维数组，二维数组的创建：

~~~python
np.array([[1,2,3],[4,5,6]])

判断ndarray的维度：

~~~
data = np.array([[1,2,3],[4,5,6]])
print(data.ndim)
~~~

返回值为2，该数组维度为2。

了解ndarray各维度的长度：

​~~~python
data = np.array([[1,2,3],[4,5,6]])
print(data.shape)
~~~

创造全是0的数组和全是1的数组：

~~~python
np.zeros(10)
np.ones((3.10))
~~~

注意多维数组各个维度的长度需要用元组来表示，(3,10)。

获取数组中某个数字：

~~~python
#一维数组
data = np.arange(10) #arange是0开始排出10个数
print(data[5]) #返回数组中的3
#二维数组
data = np.array([[1,2,3],[4,5,6]])
print(data[0][1])
print(data[0,1]) #返回第0行第1列（两个维度都是从0开始）
~~~

获取某几个数字 （切片）：

~~~python
data = np.arange(10)
print(data[3:6]) #返回345
~~~

需要注意，切片得到的数据对应原始数据，修改会反映到原始数据上。

~~~python
data = np.arange(10)
data_slice = data[3:6]
data_slice[2] = 100
print(data)

#返回 [  0   1   2   3   4 100   6   7   8   9]
~~~

需要不影响原始数据的副本：

~~~python
data[3:6].copy()
~~~

变换数组维度：

~~~python
data = np.arange(10)
print(data)
print(data.reshape((2,5))) #变为两行，每行5列

#矩阵转置
print(data.reshape((2,5)).T)
~~~

numpy常用运算：

![](https://ftp.bmp.ovh/imgs/2021/05/166e797e4d525095.png)

两个数组相加：维度不变，对应的元素相加

求和\平均值\标准差：

~~~python
print(data.sum())
print(data.mean())
print(data.std())
~~~

还有求最小最大数字，最小最大数字的值。

排序：

~~~python
data = np.array()
data.sort()
~~~

读取txt文件：

~~~python
data = np.genfromtxt('data.txt',delimiter='') #参数：文件名，分隔符号
~~~

























































