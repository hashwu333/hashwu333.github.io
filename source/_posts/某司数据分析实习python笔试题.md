---
title: 某司数据分析实习python笔试题
date: 2021-06-09 10:11:04
tags:
  - 数据科学
  - python
  - pandas
  - 笔试
categories:
  - 技术力小本本
---

某司的数据分析岗笔试，考了一道sql大题和五道pandas库小题，限时半小时。时间内其实我没有做完，可能是熟练度不够？这段时间重做了一下，pandas的小题发在这里。sql的题目有空了过段时间和另一家的sql放一起重新过一过发上来。

题目数据，是一个python字典。

~~~python
raw_data = {'platform': ['pcnews', 'pcnews', 'pcnews', 'pcnews', 'news', 'news', 'news', 'news', 'video', 'video', 'video', 'video'],
            'order_num': ['1st', '1st', '2nd', '2nd', '1st', '1st', '2nd', '2nd','1st', '1st', '2nd', '2nd'],
            'comment': [523, 52, 25, 616, 43, 234, 523, 62, 62, 73, 37, 35],
            'uv': [1045, 957, 1099, 1400, 1592, 1006, 987, 849, 973, 1005, 1099, 1523]}
~~~

### Q1：读入数据，到一个dataframe命名为content，并且将其中的列名作为dataframe的column index

使用dataframe方法即可。

~~~python
content = pd.DataFrame(raw_data) 
~~~

### Q2：筛选所有order_num = '2nd' 且platform = 'news'

~~~python
filter_1 = (content['order_num'] == '2nd') & (content['platform'] == 'news')
content.loc[filter_1,:]
~~~

### Q3： 筛选content的第2-4行和第2列之后的数据

这题我做的时候没想起来同时筛选行和列的方法，所以用了个笨法子，拆成两步，先对行进行筛选，再筛选列。但是后面查了一下，应该是用 iloc 方法。

~~~
content.iloc[1:4,1:]
~~~

### Q4：对content进行分组计算，按照platform 和order_num 对comment 求和 并按照求和结果进行降序排列

~~~python
content.groupby(['platform','order_num'])['comment'].sum().sort_values(ascending=False)
~~~

### Q5：新生成一列变量为 rank，评价标准为，当platform='news'且 comment >= 70时 rank = 'good', 当platform='pcnews'且 comment >= 500时 rank = 'medium', 其他 rank = 'worse'

~~~python
def compute_rank(row):
        if row['platform'] == 'news' and row['comment'] >= 70:
            row['rank'] = 'good'
        elif row['platform'] == 'pcnews' and row['comment'] >= 500:
            row['rank'] = 'medium'
        else: 
            row['rank'] = 'worse'
        return row

    content =  content.apply(compute_rank,axis=1)
~~~