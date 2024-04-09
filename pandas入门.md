pandas 库是一个用来进行数据操作和分析的工具

def 后面跟的-> 指的是返回值类型

参数列表中

​	参数名: 参数类型





# 创建二维列表

根据二维列表创建一个pandas 中的DataFrame 结构的数据

DataFrame 是pandas 中的二维标记数据结构

pd.DataFrame(二维列表) === 会将这个二维列表转成一个默认列名为从0 开始的列表

DataFrame 中，每一行代表一个单独的记录，每一列代表一个不同的属性

![img](image/pandas入门/1696837467-jypZMu-image.png)



使用colomns 参数，可以自定义列表的列名

这个参数需要接收一个列表，列表中存放自定义的列名

pd.DataFrame(二维列表，columns=新的列名列表)



# 获取DataFrame的大小

DataFrame 有**属性shape**，会以元组的形式返回DataFrame 的维度

shape 属性还可以返回Series的维度



![image.png](image/pandas入门/1696837772-mtKMsO-image.png)





# 返回前n行数据

head()

dataFrame.head(n) 返回前n行数据





# 获取数据

loc 属性 -- 基于标签名

iloc 属性  --- 基于索引



得到的是一个DataFrame 类型的数据

dataFrame.loc[dataFrame["索引列名称"] == 索引值, ["要返回的列名1", "要返回的列名2", ...]]

第一个索引值部分相当于是找到对应的数据行， 后面是返回的数据行的列名



# 创建新列

Series 是pandas 库提供的一维数据结构，DataFrame 中的一列数据

Series 中的所有元素是相同的数据类型

DataFrame 是以列形式显示Series

可以对DataFrame Series 中的每个单独元素执行操作



![image-20240403083703637](image/pandas入门/image-20240403083703637.png)

如果用一个系列剩一个标量，会将系列中的每个元素乘以该标量

employees['salary'] * 2 ： 会将原来的值都乘2



然后将这个结果分配给指定列

​	如果列存在就是修改，如果列不存在就会新建

​	employees['一个列名'] = employees['salary'] * 2



# 删重复行

drop_duplicates(subset, keep, inplace)

subset: 要去重的列（默认是所有列）

keep: 保留的重复行

​	first : 保留第一次出现的（默认）

​	last: 保留删除最后一次出现的

​	False: 删除所有的重复项

inplace: False: 去重后放在一个新的对象中（默认）

​		True: 在原对象中进行去重，不返回对象



# 删除丢失的数据行

dropna(axis, how, thresh, subset, inplace)

axis：0 是行， 1 是列

how：

​	any : 如果存在任何NA值，就删除该行或列

​	
