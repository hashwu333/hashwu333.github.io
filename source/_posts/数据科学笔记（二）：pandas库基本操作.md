---
title: 数据科学笔记（二）：pandas库基本操作
date: 2021-06-07 19:10:41
tags:
  - 数据科学
  - python
  - pandas
  - 笔记
categories:
  - 技术力小本本
---

### 1.数据结构

分为Series 与 DataFrame。

series为索引加数据，真正的数据只有一列。多个series结合即为dataframe。

### 2.基础类型series

#### 创建Series

~~~python
import pandas as pd

data = pd.Series([1,3,5,7])
# 也可以加入一个变量
# data = pd.Series([list_data])
print(data)
print(data.values)
print(data.index)
~~~

print输出的结果分别为：

~~~python
0    1      
1    3      
2    5      
3    7      
dtype: int64

[1 3 5 7]

RangeIndex(start=0, stop=4, step=1)
~~~

#### 特殊的索引值

创建特殊的索引值如下：

~~~python
data = pd.Series([1,3,5,7],index=['a','j','k','z'])
~~~

修改索引值名称也很简单，重新用 data.index 指定即可。

~~~python
data = pd.Series([1,3,5,7],index=['a','j','k','z'])
data.index = ['a','b','c','d']
~~~

#### 获取Series长度

~~~python
print(len(data))
~~~

#### 获取特定数据

~~~~python
data = pd.Series([1,3,5,7],index=['a','j','k','z'])
print(data['a'])
# 输出的结果为1
# 如果要获取多个特定数据，使用 print(data[['a','k','z']])
# 也可以使用切片的方式 print(data[0:2])
~~~~

#### 计算重复元素出现的个数

~~~python
print(data.value_counts())
~~~

#### 判断某个索引值是否存在

~~~python
data = pd.Series([1,3,5,7],index=['a','j','k','z'])
print('a' in data)
# return True
~~~

#### 从字典创建series

~~~python
dict_data = {
    'Beijing':1000,
    'Shanghai':500,
    'Hebei':800
}
data = pd.Series(dict_data)
~~~

#### 检测空数据

~~~python
print(data.isnull())
print(data.notnull())
~~~

#### 数组运算

~~~python
print(data*2)
print(np.square(data))
~~~

#### 设定名称

~~~python
data.name = 'xxxx'
data.index.name = 'xxx'
~~~

### 2.基础类型DataFrame

#### 创建

可以从字典直接创建。

~~~python
data = pd.DataFrame(dict_data)
data = pd.DataFrame(dict_data,columns=['a','b','c']) # 指定列顺序
~~~

#### 获取列名称

~~~python
print(data.columns)
~~~

#### 同样可以像Series一样指定索引值

#### 获取某一列数据

~~~python
print(data['student'])
print(data.student)
~~~

#### 获取某一行数据

~~~python
1.根据行编号
print(data.iloc[0])
2.根据行索引
print(data.loc['a'])
~~~

#### 数据提取：提取特定条件的行

~~~python
data = {"grammer":["Python","C","Java","GO","R","SQL","PHP","Python"],
       "score":[1,2,np.nan,4,5,6,7,10]}

df = pd.DataFrame(data)
print(df[df['grammer'].str.contains('Python')])
~~~

#### 扔掉数据

~~~python
print(data.dropna())
print(data.dropna(how='all'))

data = data.drop('d')
print(data)
~~~

#### 筛选数据

~~~python
print(data[data['score']>=90])

print(data[data['score'].isin(select_list)])
~~~

#### Group by对数据分组并计算sum,mean等

~~~python
data = pd.DataFrame({
	'tag_id':['a','b','c','a','a','c']
	'count':[10,30,20,10,10,22]
})

grouped_data = data.groupby('tag_id')
print(grouped_data.sum())
~~~

#### 数据排序

~~~python
print(data.sort_index()) # 索引升序
print(data.sort_index(ascending=False)) # 索引降序
print(data.sort_values(by='score')) # 按照某列排序，默认升序，降序加参数即可
~~~

#### 数据汇总

~~~python
print(data.sum)
~~~

#### 层次化索引

~~~python
book_ratings = pd.Series(
		np.random.randint(1,6,size=7)
		index=[
            ['b1','b1','b2','b2','b3','b4','b4']
            [1,2,1,2,1,2,3]
        ]
)
~~~

#### 合并DataFrame

~~~python
print(pd.merge(a,b))

# 不指定连接方式，会自动取交集，去掉多的value
# 可以用left，right，outer来指定
print(pd.merge(data1,data2,how='outer'))

# 指定合并的列名称
print(pd.merge(data1,data2,on='key'))

# 分别指定链接的列名称
print(pd.merge(data1,data2,left_on='lkey',right_on='rkey'))
~~~

### 3.文件交互

#### 文件存取

~~~python
# 读取csv文件(默认会把第一行作为标题)
data = pd.read_csv('rating.csv',header=None)
print(data)

# 读取csv文件，自定义标题行
data = pd.read_csv('rating.csv',names=['user_id','book_id','rating'])
print(data)

# 读取csv指定索引列
data = pd.read_csv('rating.csv',
                  names=['user_id','book_id','rating'])
				  index_col='user_id')
print(data)
~~~

#### 储存数据为csv

~~~python
data.to_csv('student.csv')
~~~

#### 读取excel文件

安装xlrd。

~~~python
file = pd.ExcelFile('xxxx.xlsx')
data = file.parse('student') #参数为表里sheet名称
~~~



