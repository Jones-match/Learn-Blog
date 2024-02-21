# 相对路径

web 中有绝对路径 和 相对路径
        绝对路径:  http://ip:port/工程名/资源路径
            不能用:     盘符:/目录/文件名

​    	相对路径:       .          当前文件所在的目录
​                   	..       当前文件所在的上一级目录
​                   	文件名     当前文件所在目录的, 相当于./文件名

javaSE 相对路径: 从工程名开始算
        绝对路径:  盘符:/目录/文件名





# 第一阶段

**界面**

## 注册界面
```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>尚硅谷会员注册页面</title>
<link type="text/css" rel="stylesheet" href="../../static/css/style.css" >
<style type="text/css">
	.login_form{
		height:420px;
		margin-top: 25px;
	}
	
</style>
	<script src="../../static/script/jquery-1.7.2.js"></script>
	<script type="text/javascript">
		$(function () {
			//绑定单击事件
			//用户名验证
			$("#sub_btn").click(function () {
				//1.获取用户名输入框的内容
				var username = $("#username").val();
				//2.创建正则表达式
				var usernamePatt = /^\w{5,12}$/;
				//3. 验证
				if (!usernamePatt.test(username)) {
					//4. 提示用户结果
					$("span.errorMsg").text("用户名输入有误");
					return false;
				}
				$("span.errorMsg").text(""); //合法后要去掉错误信息

				//密码验证
				var password = $("#password").val();
				var passwordPatt = /^\w{5,12}$/;
				if (!passwordPatt.test(password)) {
					$("span.errorMsg").text("密码格式有误");
					return false;
				}
				$("span.errorMsg").text("");

				//确认密码的验证
				var repwd = $("#repwd").val();
				if (!(password == repwd)) {
					$("span.errorMsg").text("确认密码与密码不一致");
					return false;
				}
				$("span.errorMsg").text("");

				//邮箱验证
				var email = $("#email").val();
				var emailPatt = /^\w{3,12}@\w+.com$/;
				if (!emailPatt.test(email)) {
					$("span.errorMsg").text("邮箱格式有误");
					return false;
				}
				$("span.errorMsg").text("");

				//验证码验证
				var code = $("#code").val();
				//去掉前后的空格
				code = $.trim(code);
				if (code == null || code == "") {
					$("span.errorMsg").text("请输入验证码");
					return false;
				}
				$("span.errorMsg").text("");
			});
		});
	</script>
</head>
<body>
		<div id="login_header">
			<img class="logo_img" alt="" src="../../static/img/logo.gif" >
		</div>
		
			<div class="login_banner">
			
				<div id="l_content">
					<span class="login_word">欢迎注册</span>
				</div>
				
				<div id="content">
					<div class="login_form">
						<div class="login_box">
							<div class="tit">
								<h1>注册尚硅谷会员</h1>
								<span class="errorMsg"></span>
							</div>
							<div class="form">
								<form action="regist_success.html">
									<label>用户名称：</label>
									<input class="itxt" type="text" placeholder="请输入用户名" autocomplete="off" tabindex="1" name="username" id="username" />
									<br />
									<br />
									<label>用户密码：</label>
									<input class="itxt" type="password" placeholder="请输入密码" autocomplete="off" tabindex="1" name="password" id="password" />
									<br />
									<br />
									<label>确认密码：</label>
									<input class="itxt" type="password" placeholder="确认密码" autocomplete="off" tabindex="1" name="repwd" id="repwd" />
									<br />
									<br />
									<label>电子邮件：</label>
									<input class="itxt" type="text" placeholder="请输入邮箱地址" autocomplete="off" tabindex="1" name="email" id="email" />
									<br />
									<br />
									<label>验证码：</label>
									<input class="itxt" type="text" style="width: 150px;" id="code"/>
									<img alt="" src="../../static/img/code.bmp" style="float: right; margin-right: 40px">									
									<br />
									<br />
									<input type="submit" value="注册" id="sub_btn" />
									
								</form>
							</div>
							
						</div>
					</div>
				</div>
			</div>
		<div id="bottom">
			<span>
				尚硅谷书城.Copyright &copy;2015
			</span>
		</div>
</body>
</html>

```



# 第二阶段

实现用户的**注册和登陆**



客户端（浏览器） + JavaEE + 数据库



## JavaEE 三层架构

1. Web 层 （视图展现层）
    	1. 获取请求的参数，封装成Bean 对象
    	1. 调用Service 层处理业务
     	3. 页面回传数据
              	1. 请求转发
                   	2. 重定向

    
    Servlet程序
    
    
    
2. Service 层（业务层）
    1. 处理业务逻辑
    1. 调用持久层保存到数据库

	Spring 框架
	
	
	
	1 个业务1 个方法
	
	
	
3. Dao 持久层（将数据写到数据库）
    1. 只负责与数据库交互（CRUD：Create, Read, Update, Delete)

​	JDBC

​	DBUtils

​	JDBCTemplate

​	

![image-20240124200322518](image/proj-bookstore/image-20240124200322518.png)



不同的层级有不同的包

| Web 层        | com.atguigu.servlet/web/controller  | Servlet 程序       |
| ------------- | ----------------------------------- | ------------------ |
| Service 层    | com.atguigu.service                 | Service 接口包     |
|               | com.atguigu.service.impl            | Service 接口实现类 |
| DAO层         | com.atguigu.dao                     | DAO接口包          |
|               | com.atguigu.dao.impl                | DAO 接口实现类     |
| 实体Bean 对象 | com.atguigu.pojo/entity/domain/bean | JavaBean 类        |
| 测试包        | com.atguigu.test/junit              |                    |
| 工具类        | com.atguigu.utils                   |                    |



编码流程 不同于 软件设计流程 

## 整体流程

1. 先创建数据库和表

2. 编写数据库对应的JavaBean 对象 

    有一个user类与数据库的表对应

    里面的属性对应于表中的各个列名
    
    设置getter setter constructor toString 这几个部分
    
    
    
    

​	编写之前项目经理应该会有一个Util 工具类

​	编写DAO 层（需要访问数据库）---> 需要编写工具类JDBCUtils

​				-----> 还要写一个BaseDao



3. 🤢 编写JDBCUtils 类 ---> 用于管理数据库的连接池
    1. 获取连接
    2. 关闭连接



​	编写JdbcUtils的测试类，@Test 是要导入这两个包

![image-20240130184812716](image/proj-bookstore/image-20240130184812716.png)



4. BaseDao 

5. 编写具体的Dao 和测试
    1. UserDao
        1. *为什么这个UserDao 是一个接口？*

​	

​	新的测试方法： 在接口类中，Ctrl + Shift + T 



6. 编写UserService 和测试
7. 编写web 层
    1. 共有两种功能 
        1. 用户登录  用户注册














### JdbcUtils 的编写流程

目的是为了管理数据库的连接池

（1）先写这个类里面需要什么方法

​	a. 获取连接  getConnection()

​	b. 关闭连接 close(Connection connection)

（2）根据这个方法框架来完成整个类的编写



a. 先将返回值全部设为空，只是搭一个框架

b. 导入需要的包

c. 初始化连接

​	1、首先知道需要一个DataSource	

​		使用静态代码块完成初始化

​	2、 使用DruidSourceFactory.createDataSource(）创建连接池

​		 这里就要使用一个properties 对象参数

​	3、 properties 对象需要读取自己的文件 (从流中加载数据)

​		使用load 方法加载一个流

​		流 --  JdbcUtils.class.getClassLoader().getResourceAsStream(路径)

​				这里的路径默认是从src 开始的(不用写 /)

​				properties 放在src 这个目录里面， 和com 在同一级

d. 实现获取连接的方法

e. 实现关闭连接的方法





​				

### BaseDao 的编写流程

BaseDao 里面是为了给其他人进行复用（继承）的， 不用写对象实例

----> 设置成抽象类



使用DbUtils 操作数据库

QueryRunner 



update() : 返回值是影响的行数， 如果是-1 代表是执行失败

​		主要用于Update, Delete, Insert

​	queryRunner.update(); ====>  第三个参数是代表查询语句中的占位符？ 所在的位置， 使用一个可变参数来传



查询返回一个JavaBean 

queryForOne(): 

​		queryRunner.query()	传入一个new BeanHandler<>();

查询返回多个对象

queryForList(): 

​		与一个对象的情况，只有传入的对象不同	new BeanListHandler<>()

查询返回一个值Scalar



ScalarHandler: 表示单行单列的查询结果

BeanHandler:表示把**结果集中的一行数据，封装成一个对象**，专门针对结果集中只有一行数据的情况。

BeanListHandler:表示把结果集中的**多行数据，封装成一个对象的集合**，针对结果集中有多行数据。



<T>List<T> 

第一个T就是振臂一呼，告诉大伙，哥是个类型，以后见到别不认识我。

第一个T 代表是一个泛型，第二个与List 组合在一起的List<T> 代表的返回类型是一个List，这个List 中放的对象类型是T 所指的类型





### UserDao 的编写流程

考虑在网页的访问过程中，与User 相关的**数据库操作**有哪些：

- 注册时：
    - 查询用户名是否存在
    - 将用户信息保存在数据库中
- 登录时：
    - 查询用户名和密码是否正确

​	

### UserDaoTest 的编写方法

测试哪个模块，就在Test 中新建一个对象

然后在方法的对应test 方法中，使用新建的对象来调用要测试的方法

检查方法的输出是否合理



![image-20240131100133395](image/proj-bookstore/image-20240131100133395.png)



### UserService 的编写流程

Service 是业务层，一个业务一个方法

看这个User 会有哪些方法： 

​	登录

​	注册

​	检查用户名是否存在

​	

### web 的编写流程

注册 的思路： 

​	服务器需要有一个Servlet 程序接收网页上提交的表单请求



![image-20240131174719590](image/proj-bookstore/image-20240131174719590.png)

​	1、 创建一个Servlet 程序 并 配置好地址

​	2、 修改html 页面上的表单的action 所指的地址（action 里面不带/） 

​			修改base 地址

​			action 是提交表单的时候要发送的地址



<font color="red" size=5>还是不太理解</font>

​	form 里面的action 加/ 和不加/ 表示的是哪里，怎么能够找到servlet程序

​	<font color="darkviolet" size=4>加上/ 之后（例如/testFile)，指的是`http://ip:port/testFile` <br/>	如果不加/ ， 就是`http://ip:port/工程路径/testFile`</font>

​	

​	



## 导入第三方包方法

（1）所有加进来的第三方包，都要放在bookstore(工程目录) -> web -> WEB-INF -> lib 中

（2）加进项目的方法：

a.  Project Structure -> libraries ->  + ->Java -> 找成自己放在lib 中的jar包 -> 修改这个Library 名字 

b. Modules -> 工程名 -> Dependencies -> + -> Library

c. Artifacts -> Fix

d. Apply ✔





## 文件放的位置

（1）所有加进来的第三方包，都要放在bookstore(工程目录) -> web -> WEB-INF -> lib 中

（2）数据库需要的properties 文件，要放在src 这个目录里面， 和com 在同一级

原因：

​	使用了这个方法获取：  Class.getClassLoader.getResourceAsStream(String path) ：默认则是从ClassPath根下获取，path不能以’/'开头，最终是由ClassLoader获取资源。 

​	具体解释：

​	https://www.cnblogs.com/macwhirr/p/8116583.html





# 第三阶段

<font size=5>**优化**</font>

注册失败添加提示信息

改成jsp页面后方便回写提示信息 ---- 方便输出内容



## 改jsp文件

html 页面最上面一行添加page 标签

改成jsp 后缀

​	*按照目录进行替换*

![image-20240216115837225](image/proj-bookstore/image-20240216115837225.png)



## 抽取页面中相同的内容 





## 动态获取ip 地址

href 里面的地址要用表达式脚本



使用request 对象里面的相应方法，获取地址中的每个部分

​	http, ip, port, 工程路径..





## 显示错误信息





## BaseServlet 抽取

一般一个模块只会使用一个Servlet程序



request.getParameter() 方法可以获取指定name的value值（只要是value指定了，就可以获取）

​	因此，可以用input:hidden 使用不同的value来分出不同的功能



用反射来根据不同的请求得到不同的处理方法

```java
method = servletProgram.class.getDeclaredMethod(methodname, 后面是方法需要的参数(Class.class类型，指明参数是什么类型));
		this.getclass().getDeclaredMethod()
		获取当前类的类型
            
method.invoke(new servletProgram())  意思是调用servlet中的method 方法  
    	invoke(this, req, resp) 使用当前这个对象实例this, 调用方法时需要传入两个参数req, resp
            
```



每一个模块都是：

1、 获取action 参数

2、 通过反射获取对应的方法

3、 通过反射调用方法



## BeanUtils 

数据封装和抽取

一次性将所有的请求参数注入到JavaBean 中

第三方包

![image-20240217100656202](image/proj-bookstore/image-20240217100656202.png)

BeanUtils.populate(bean对象，传的多个参数构成的map(使用request.getParameterMap()))

注入是靠相应的属性名的setter方法，将参数名改成setXXX() 方法，然后将值设置好



写的是Map 参数可以在Dao, Service 层使用这个工具

耦合更低

使用HttpServletRequest 耦合很高



# 第四阶段

<font size="5"><b>使用EL 回显信息</b></font>

EL 表达式在参数值为空时，自动输出空串





# 第五阶段

图书模块



## MVC

| view       | 视图   | Jsp/html | 显示界面                    |
| ---------- | ------ | -------- | --------------------------- |
| controller | 控制器 | Servlet  | 处理代码请求，派发页面      |
| model      | 模型   | JavaBean | 将数据封装在一个JavaBean 中 |

最早出现在web 层

目的是为了解耦合

将软件代码拆解成组件，单独开发 



## 开发流程

数据库 ---> JavaBean ---> Dao ---> Service ---> Web



在页面上访问图书管理，不能直接去jsp页面中，因为此时页面中还没有数据

​		jsp是属于客户端，不能直接查询数据库

应该向Servlet层发送请求，让Servlet 通过Service 来调用Dao 实现查询数据

Servlet将查到的图书信息保存到Request 域中，通过请求转发带着数据打开jsp页面

​	jsp页面此时再将所有的信息展示出来

​		使用JSTL 标签遍历输出



**如果直接访问jsp页面得不到数据，可以先访问Servlet 程序之后再转发**

<img src="image/proj-bookstore/image-20240217120447216.png" alt="image-20240217120447216" style="zoom:80%;" />



这里加上/manager 是为了方便之后进行权限管理



前台是给普通用户使用

​	一般不需要权限检查就可以访问的资源或功能

​	

后台是给管理员使用的

​	一般都需要权限检查才可以访问的

​	

通过地址来区分前台，后台



## 页面中的功能

添加，删除，修改，显示页面



### 添加

**添加图书会出现表单重复提交**

​	当用户完成提交请求，浏览器会记录下最后一次请求的全部信息

​	当用户按下F5就会发起浏览器记录的最后一次请求----添加操作

​		因此需要使用重定向转发到显示图书的界面

```java
resp.sendRedirect()
```

请求转发/ 是表示工程路径

重定向/ 是表示端口

因此地址需要添加一个工程名

```java
resp.sendRedirect(req.getContextPath() + "/manage/bookServlet?action=list");
```



重定向之后，再按F5之后，最后一次请求就是list 这个请求，不会是add+list

在使用请求转发的时候，add + list 是在一次请求中完成的，因此浏览器保存最后一次请求的所有信息，会包括add 这一步

而在使用重定向时，add 是第一次请求，list 是第二次请求，浏览器保存最后一次请求的所有信息，就是第二次发起的list 请求

​	这个时候按下F5，他只会执行list 这一步操作，而不会执行第一步的add 步骤



### 删除



### 修改





### 分页

244
