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

实现用户的注册和登陆



客户端（浏览器） + JavaEE + 数据库



JavaEE 有三层架构

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
	
	
	
3. Dao 持久层（将数据写到数据库）
    1. 只负责与数据库交互（CRUD：Create, Read, Update, Delete)

​	JDBC

​	DBUtils

​	JDBCTemplate

​	

![image-20240124200322518](image/书城项目/image-20240124200322518.png)



不同的层级有不同的包

| Web 层        | com.atguigu.servlet/web/controller  |                    |
| ------------- | ----------------------------------- | ------------------ |
| Service 层    | com.atguigu.service                 | Service 接口包     |
|               | com.atguigu.service.impl            | Service 接口实现类 |
| DAO层         | com.atguigu.dao                     | DAO接口包          |
|               | com.atguigu.dao.impl                | DAO 接口实现类     |
| 实体Bean 对象 | com.atguigu.pojo/entity/domain/bean | JavaBean 类        |
| 测试包        | com.atguigu.test/junit              |                    |
| 工具类        | com.atguigu.utils                   |                    |



编码流程 不同于 软件设计流程 

1. 先创建数据库和表

2. 编写数据库对应的JavaBean 对象 

    有一个user类与数据库的表对应

    里面的属性对应于表中的各个列名
    
    设置getter setter constructor toString 这几个部分
    
    
    
    

​	编写之前项目经理应该会有一个Util 工具类

​	编写DAO 层（需要访问数据库）---> 需要编写工具类JDBCUtils

3. 🤢 编写JDBCUtils 类 ---> 用于管理数据库的连接
    1. 获取连接
    2. 关闭连接





## JdbcUtils 的编写流程

（1）先写这个类里面需要什么方法

​	a. 获取连接

​	b. 关闭连接

（2）根据这个方法框架来完成整个类的编写

a. 先将返回值全部设为空，只是搭一个框架

b. 导入需要的包

c. 初始化连接

​	1、首先知道需要一个DataSource，





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



