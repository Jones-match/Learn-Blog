在python 的编译器中，上一个表达式的输出会保存到 _ 这个变量中

![image-20240331192737948](image/python入门/image-20240331192737948.png)



# 输入

一次性读取多个数据

```python
x, y = [int(i) for i in input().split()]
# 会将input 按空白符切割，并转换成一个列表
# 使用for 对输入列表进行遍历，同时对每个数据进行强转
# 遍历之后的数据，构成一个新的列表 
# x 取列表中的第一个数据
# y 取列表中的第二个数据 
# 

```









# 输出格式化

print("%.2f" %num)



print("{1}, {0}".format("索引为0 的值", "索引为1 的值"))

花括号中的数字表示format 中的索引



print("字符串中的其他信息 {name1}, {name2}".format(name2="值1", name1="值2"))

会按照名字进行填充



print("{:.2f}".format(123.2222))

控制小数位数



print(str.upper())	大写

print(str.lower())	小写	

print(str.title())	首字母大写

print(str.strip())	去掉字符串两边的空白符

print(str * 10)		可以重复输出10 次字符串

print(str[0:10])		取前10 个字符 （0 ~ 9）

# 数据类型

int, float, bool, complex



int(输入的字符串, base=进制数)

进制数默认为10



int() 可以将括号内的数据进行强转



## 列表

remove("删除指定的元素")

append("追加元素")

insert(index, 元素) 会在index 位置上插入一个新的元素

pop() 删除列表的最后一个元素，可以指定索引值

sort(key=不知道是什么, reverse=False(升序，默认)|True(降序))

newlist = sorted(list) 可以临时排序list，不会改变list 中的值

list.reverse()  会将列表倒序



列表如果为空，对应的布尔值为False，因此可以直接用于判断



判断元素是否在列表中：

ele in List



+号会进行列表的拼接

*会重复列表



## 字符串

切分

list = str.split("分隔符")

```
# 如果num 有指定值，最终会分割为num + 1 个字符串
str.split(str="", num=string.count(str))
```





### 大小规则

常见ASCII码的大小规则：0～9　<　A～Z　<　a～z。
1）数字比字母要小。如 “7”<“F”；
2）数字0比数字9要小，并按0到9顺序递增。如 “3”<“8” ；
3）字母A比字母Z要小，并按A到Z顺序递增。如“A”<“Z” ；
4）同个字母的大写字母比小写字母要小32。如“A”<“a” 。
几个常见字母的ASCII码大小： “A”为65；“a”为97；“0”为 48

使用== 判断两个字符串是否相等



# 位运算

&

|

