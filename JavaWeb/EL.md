# 起到的是输出功能

EL 表达式不需要导入其他的包就可以使用

JSTL需要在页面头导入

全称是Expression Language 表达式语言

主要是替代jsp 页面中的表达式脚本在jsp 页面中进行数据的输出



EL 输出会比jsp 中的简洁

```jsp
表达式脚本:
<%= request.getAttribute(name) %>

EL: 
${name}

```

当数据不存在的时候， 

​	**EL 表达式会输出空串 -- 输出就没有东西 **

​	**而表达式脚本会输出null 字符串**





**EL主要是输出域对象中的数据**



搜索域的顺序 是 从小到大



输出对象：直接用${对象}就会输出toString() 方法

输出数组类型的数据：默认是输出数组元素的地址，使用[] 可以输出指定下标的元素

输出List类型的数据：默认是输出整个List 中的所有元素，使用[] 可以输出指定下标的元素

输出Map 类型的数据：默认是输出整个Map 中的所有键值对，使用 map.键名 可以输出**指定的键值对**

​	map 中的每个项都是一个entry 键值对

​		entry.value 可以取出map对应的值



**${} 中，输出的属性名是找对应的get 方法，只要有对应的get 方法就行，没有这个属性是无所谓的**



# 运算：

${运算表达式}

 

## 关系运算

可以使用和java 中一样的比较运算符



## 逻辑运算 

与java 一样 



## 算术运算

\+ \- \* / %

除法运算是浮点结果



## empty 运算

可以判断一个数据是否为空

如果为空则输出true，否则输出false

```jsp
$ {empty 数据 } 
```





true 的情况：

值为null

值为空串

值为Object 类型数组，且长度为0

List 集合，且个数为0

Map 集合，且个数为0





## 三元运算



## 点运算 和 中括号运算

点运算： 可以输出 Bean 对象中的某个属性的值

中括号运算： 可以输出有序集合中某个元素的值

​	且中括号运算还可以输出map 集合中key 中含有特殊字符的key 值

​	$ {map['key 名']} 或 $ {map["key 名"]}

​	单双引号都可以



# 11 个隐含对象

EL 表达式中自己定义的，可以直接使用

| 变量             | 类型                    | 作用                                          |
| ---------------- | ----------------------- | --------------------------------------------- |
| pageContext      | PageContextImpl         | 可以获取jsp 中的九大内置对象                  |
|                  |                         |                                               |
| pageScope        | Map<String, Object>     | 可以获取pageContext 域中的数据                |
| requestScope     | Map<String, Object>     | 可以获取request 域中的数据                    |
| sessionScope     | Map<String, Object>     | 可以获取session 域中的数据                    |
| applicationScope | Map<String, Object>     | 可以获取servletContext 域中的数据             |
|                  |                         |                                               |
| param            | Map<String, String>     | 可以获取请求参数的值                          |
| paramValues      | Map<String,  String[]>  | 获取多个值的时候使用(checkbox)                |
|                  |                         |                                               |
| header           | Map<String, String>     | 获取请求头的信息                              |
| headerValues     | Map<String, String[]>   | 获取多个值的情况                              |
|                  |                         |                                               |
| cookie           | Map<String, Cookie对象> | 可以获取当前请求的cookie 信息                 |
|                  |                         |                                               |
| initParam        | Map<String, String>     | 可以获取在web.xml 中的配置<context-param>参数 |



## pageContext 的用法

大部分是在pageContext.request 中

在jsp 中，使用`<%=request.getXXXX()%>`, 而到了EL表达式中，去掉get 放到request.的后面就行 ${pageContext.request.XXXX}

### 协议

在jsp 语法中，request.getScheme() 可以得到协议信息

而在EL 表达式中，使用 ${pageContext.request.scheme}



### 服务器ip

request.getServerName()

在EL 表达式中： ${pageContext.request.serverName}



### 端口

serverPort



### 工程路径

contextPath



### 请求方法

method



### 客户端的IP 地址

remoteHost



### 会话的ID 编号

session.id



## Param 相关对象

如果只有一个值，推荐使用param

如果有多个值，param不能使用了，就得使用paramValues 获取



## header 相关对象

${header["user-agent"]}

如果有多个值就得使用headerValues 获取



## cookie 相关对象

${cookie.jssesionid.name} 获取 cookie 的名字

${cookie.jssesionid.value} 获取cookie 的值





## initParam

