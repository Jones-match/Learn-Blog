异步Javascript 和XML

Asynchronous Javascript And XML



ajax是浏览器通过js异步发起请求，局部更新页面的技术



使用Javascript发起Ajax请求，访问服务器步骤：

1。创建XMLHttpRequest 对象

2。使用对象的Open方法设置请求参数

​	请求类型，url，是否是异步请求

3。在使用send 方法前，绑定onreadystate事件

4。使用Send方法向服务器发送请求

5。服务器返回响应

​	将变量对象转成Json发送给客户端

6。从onreadystatechange事件中进行判断， 当readystate == 4 && status == 200

​	客户端使用XMLHttpRequest对象的ResponseText 属性获取字符串形式的值

​								ResponseXML 属性获取XML形式



浏览器的响应乱码，可以使用response 中的setContentType设置

```java
response.setContentType("text/html; charset=utf8");
```



指定响应放入的标签：

```html
document.getElementById("id值").innerHTML = xmlHt
```





局部更新：

浏览器的地址栏不会发生变化

局部更新不会改变原来的内容



异步请求：

服务器没有处理Ajax请求，就不会继续执行下面的代码（同步）

​	发起一个网页请求，整个页面就会卡死





# JQuery 中的Ajax请求

点击事件

```html
$("")		绑定一个按钮
$("").click(functin() {

}) 
```

在点击按钮之后，执行function 这个函数里面的功能





## $.ajax 方法

url 请求地址

type 请求的类型(Get, Post)

data 发送给服务器的数据（参数信息）

​	有两种格式

​	name1=value1&name2=value2

​	{key1:value1}

success 请求成功，响应的回调函数

​	在success的函数中，要写一个参数接收服务器传过来的数据

​	想要提取一些属性内容，要先将传过来的数据转成Json格式

​		然后Json.属性 取出想要的属性对应的值



Type 数据类型

​	响应的数据类型

​	常用的数据类型有：

​		text 纯文本 

​		xml  xml 数据

​		json  Json数据



```html
$.ajax({url: xxx, data: xxx, })
```



## $.get() && $.post()

url 请求的URL 地址

data 发给服务器的数据（参数信息）

callback 响应后的回调函数

type 响应的数据类型



## $.getJSON()

通过GET 获取Json数据

url

data 参数列表  action=Servlet.xxx() 中的xxx方法名

callback



## serialize()



获取表单中的所有的表单项

并以name=value 的形式进行拼接 ---- 就是一个参数



之前提交时，整个页面都进行提交









