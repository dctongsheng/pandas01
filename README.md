# pandas01
前言：
pandas是在numpy的基础上开发出来的，有两种数据类型Series和DataFrame
Series由一组数据（**numpy的ndarray**）和一组与之相对应的标签构成
DataFrame表格行的数据结构，包含一组有序的列
#Series
* ## 何为Series？
Series由一组数据（**numpy的ndarray**）和一组与之相对应的标签构成
* ##创建Series
```
from pandas import Series,DataFrame
import pandas as pd
ser01=Series([1,2,3],index=['n','m','j'])
#通过字典的形式创建
ser02 = Series({3:"a",4:'b',5:"c"})
```
* ##索引切片
```
ser02[0:2]
ser01["n"]
```

* ##运算
类似ndarray运算
```
print(ser01[ser01>=2])#注意输出值用中括号括起来
print(ser01>=2)
ser01+10
np.exp(ser01)
np.fabs(ser01)#绝对值
```
* ##缺失值处理
```
ser02=Series(ser01,index=['n ','m','j','q'])
pd.isnull(ser02)
#过滤掉np.nan的值
ser02[pd.notnull(ser02)]
```
* ##自动对齐
```
#自动对齐，把相同的index相加
ser03=Series([1,2,3,4],index=['n','h','m','t'])
ser02+ser03
```
#DataFrame
* ##何为DataFrame？
DataFrame表格行的数据结构，包含一组有序的列，有行、列索引，可以看做是Series的字典组成
* ##创建DataFrame
```
df01 =DataFrame([['susan','long','meimei'],[50,60,60]],index=['姓名','成绩'],columns=['语文','math','english'])
df01
#用字典创建,字典为列索引
dict={
    "apart":[121,111,144,122],
    "year":[2011,2013,2022,2003],
    "month":8,
    "profit":[100,22,99,80]
}
df02=DataFrame(dict,index=['one','two','three','four'])
df02
```
* ##通过行列数据获取
默认为列获取，如果获取行可用pd.loc()
```
df02['apart']
#列增加
df02['address']=['北京','shanghai','shuangzhou','shenzhen']
df02
#列删除
df02.pop('apart')
df02['month']=3
#行操作
df02.loc['two']
```
* ##读取文件
```
分别读取csv、excel、txt文件
df04=pd.read_csv('data.csv')
df05=pd.read_excel('data.xlsx')#excel
df03 = pd.read_csv("data.txt",sep="\t",header=None)
```
* ##过滤切片
```
df05.columns[1:]
df05[df05.columns[1:]]
df1=df02.dropna(axis=1)#
```
* ##缺失值操作
和series类似
```
df04.isnull()
#删除缺失值
df04.dropna(axis=1)#axis=1为去一列，默认为去一行，注意和数学统计里面默认计算的列不一样
df04.dropna(how="all")
#替换缺失值
df04.fillna(0)
df04.fillna({0:1,1:2,2:3})
```
* ##数学统计
常见的方法如count describe min/max idxmin、idxmax quantile sum mean median mad var std cumsum pct_change
```
df02.describe()
df1=df02.dropna(axis=1)
df02.quantile(0.25)#计算样本分位（0到1）
df02.median()#中位数
df02.pct_change()#计算百分比变化
```

* ##协方差和相对系数
直观反应两组数据的相关程度分别为cov，corr
```
df2=DataFrame({
    "gdp":[2,4,6],
    "chukou":[3,2,1]
})
df2.cov()
df2.corr()
```
* ##唯一值，值计数，成员资格
唯一值unique，值计数value_counts，成员资格isin（等于用没里面的元素来过滤）
```
df3=Series([12,13,14,15,13,13,12,11,14])
df3.unique()
df3.value_counts()
df3[df3.isin([14,15])]#成员资格
```
* ##层次索引
```
索引可以大于一维，unstack(level=1)可把series转化为dataframe，swapleve转换索引
df.set_index([])

```
后记：
*才疏学浅，慢慢学习，慢慢更新，与诸君共勉*

*你可能感冒的文章：
[我的机器学习numpy篇](https://www.jianshu.com/p/3a757f14a713)
[我的机器学习matplotlib篇](http://www.jianshu.com/p/f2ebf312e323)
[我的机器学习微积分篇](https://www.jianshu.com/p/cd7110333d75)*

