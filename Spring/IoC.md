# 概述

是一种<font color="red" size=5>设计思想</font>，可以设计出松耦合的优良程序

Spring通过IOC容器管理所有Java对象的实例化和初始化，控制对象与对象之间的依赖关系

​	A 类对象调用B 类对象中的方法，不需要再去new B() 之后再去调用方法了，而是改成由IOC容器进行管理

​	

IOC管理的Java对象是Spring Bean 



IOC容器：

​	管理容器内的对象的生命周期中的完整过程





告诉IOC我要创建什么对象，我需要维护一个什么样的关系，具体的实现由IOC容器去完成





容器中放的是Bean对象， 使用的是Map集合

​	key-value 是很方便完成存-取操作





## 原理

1、在xml中写好需要的Bean定义的相关信息

2、通过 BeanDefinitionReader 接口来进行读取

3、在IOC容器中就会加载一个Bean定义信息，通过BeanFatory 和 反射 来进行实例化，并进行初始化之后可以得到最终对象

![image-20240309201024211](image/IoC/image-20240309201024211.png)



## 依赖注入

DI：实现了控制反转

Spring 在创建对象的过程中，将<font color="red" >**对象依赖属性？？？？？**</font>通过配置进行注入

​	**什么是对象依赖属性？**

依赖注入：在创建对象的过程中，给属性设置值



两种常见的注入方式：

1、 set

​	

2、 构造注入

​	





## Bean管理

**对象的创建过程**以及**属性的注入**合在一起称为Bean管理 





BeanFactory工厂 

IOC最基本的实现，是Spring内部使用的，开发者并不能使用

用户需要使用该接口的子接口ApplicationContext  

![image-20240309200744451](image/IoC/image-20240309200744451.png)

 子接口中的实现类：

| 方法                            | 内容 |
| ------------------------------- | ---- |
| ClassPathXmlApplicationContext  |      |
| FileSystemXmlApplicationContext |      |
| ConfigurableApplicationContext  |      |
| Web                             |      |





### 基于XML 管理bean

父工程中写的xml 配置文件，子模块中的xml 中就不用再写了



搭环境：建模块，配置xml文件



#### 获取bean的三种方式

三种方式获取到的bean 是同一个bean

1、根据id 获取 

```xml
<bean id="自定义id" class="全类名"></bean>
```

```java
ApplicationContext context = new ClassPathXmlApplicationContext();
context.getBean("id 值");
```



2、根据类型获取

```java
context.getBean(User.class);
```



3、根据id 和类型获取

```java
context.getBean("id值", User.class);
```



根据类型获取bean 时

1：IOC 容器中指定类型的bean有且只能有一个（不能在xml 中给一个class 配置多个不同的id 的bean 标签）

2：对于一个接口，根据接口.class 获取，如果只有一个实现类，可以获取bean （使用instanceOf判断是不是一个接口的实现）

​			如果有多个实现类，无法获取bean

#### 依赖注入

类里有属性，创建对象过程中，给属性设置值

1、 使用setter 注入

创建类，并设置set方法

在Spring配置文件中配置 

```xml
<bean id="自定义值" class="全类名">
	<property name="属性名" value="给属性值"></property>
  	会自动调用类中的setXxx() 方法
</bean>
```



2、 使用构造器注入

```xml
<bean id="" class="">
    根据属性名和value 来调用构造器
	<constructor-arg name="" value=""></constructor-arg>
    
    <constructor-arg index="" value=""></constructor-arg>
</bean>
```

如果在xml 文件中创建了set方法的注入，在加载xml 文件时会自动执行一次参构造器



3、 特殊值注入

- 字面量赋值 -- 会将标签中的value 属性当作是一个字面量

- null 值 -- 在property 中写一个null 子标签(两种方法都可以)

`<property name="属性名"><null></null></property>`

`<property name="属性名"><null/></property>`

- xml 实体

`&lt;` 等进行**转义**

- CDATA节

在CDATA 区中可以写特殊的需要转义的符号

```xml
<property name="">
	<value><![CDATA[a < b]]></value>
</property>
```



4、 特殊类型的属性注入

1）对象类型

- 引入外部bean

创建两个类的对象 : dept 和 emp

在emp 的bean标签中，使用property 引入dept 的bean

```xml
<bean id="" class="">
	<property name="对象属性名" ref="类在bean 中的id值"></property>
</bean> 
```

就会调用在xml 中创建的外部bean



- 内部bean

将想引用的类的bean 标签写在当前的bean 标签里的property 标签中

```xml
<bean id="" class="">
	<property name="对象属性名">
    	<bean id="" class="">
        	<property name="" value=""></property>
        </bean>
    </property>
</bean> 
```



- 级联属性赋值

 给引用的bean 的类的属性进行赋值

```xml
<bean id="" class="">
	<property name="对象属性名dept" ref="类在bean 中的id值"></property>
    <property name="dept.dname" value="新的值"></property>
</bean> 
```





2）数组类型

```xml
<property name="数组类型属性名" >
	<array>
    	<value>第一个元素</value>
        <value>2</value>
    </array>
</property>
```



3）集合类型

- List类型 

```xml
<property name="集合类型属性名">
	<list>
		<ref bean="外部类id">list 中第一个对象类型元素</ref>
		<ref bean="外部类id">list 中第二个对象类型元素</ref>
        如果是字符串类型，可以直接使用value 标签中写值即可
        <value>值</value>
    </list>
</property>
```



- Map类型

```xml
<property name="map 属性名">
	<map>
    	<entry>
        	<key>map 中的key</key>
            
            map 中的value
            <value></value>
            或 
            <ref bean="外部类id"></ref>
            
        </entry>
    </map>
</property>
```



数组类型和集合类型，相当于把value 和 ref 标签从property 中拿出来，构成多个值



4）引用集合类型的bean

使用标签util:类型 定义集合类型的属性值

util:list 标签中的id 值与注入时引用的值是一样的





**util 标签会报红的原因：**

schema约束中没有util 这个标签的约束

引入这个相应的命名空间就可以使用util 这个标签了

```xml
1。 在文件头的beans 标签中，加入相应的属性

xmlns:uti="http://www.springframeword.orgschema/util"

2。 然后在xsi:schemaLocation 属性中，加上util 需要的链接
"http://www.springframework.org/schema/util/spring-util.xsd
http://www.springframework.org/schema/util
"
```





#### p命名空间

xmlns:p 

p用来避免标签中属性名字的冲突



在注入的时候，不用property 子标签进行属性设置

改用在bean 标签中，加上标签属性p:类的属性名="属性值"



通过使用p:属性名来完成属性的注入

如果是一个对象类型的值，就需要在属性名后加上-ref

```xml
p:teacherMap-ref="teacherMap"
```

这时，等号的右边写得就是id值



#### 引用外部属性文件

所需要的特定固定值放在一个外部文件中

引用外部文件后做到属性注入



之后做修改的时候，只用改外部文件中的内容，而在spring 的配置文件中不会再发生改动



在spring 中只需要引用



数据库场景：

- 引入数据库相关依赖

```xml
    <dependencies>
        <!-- MySQL驱动 -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.30</version>
        </dependency>
        <!-- 数据源 -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.2.15</version>
        </dependency>
    </dependencies>
```



- 创建外部属性文件

```properties
jdbc.user=root
jdbc.password=root
jdbc.url=jdbc:mysql://localhost:3306/spring?serverTimezone=UTC
jdbc.driver=com.mysql.cj.jdbc.Driver
```



- 在spring配置文件中引入**context 命名空间**引入属性文件，使用表达式完成注入

改文件头信息，引入命名空间

使用命名空间中的context 标签

```xml
<contex:property-placeholder location="classpath:jdbc.properties">
表示将类路径下的jdbc.properties 文件引入进来</contex:property-placeholder>
```

注入

```xml
<bean id="" class="">
    //可以从配置文件中读入url
	<property name="url" value="${jdbc.url}"></property>
</bean>
```





#### bean 的作用域

可以使用bean 标签中的scope 属性来指定bean 的作用域

singleton  单实例 （默认）

​		在IOC 容器初始化的时候创建

​		`ApplicationContext context = new ClassPathXmlApplicationContext("xxx.xml")` 执行时就会创建实例化对象

prototype  多实例

​		在获取bean  的时候创建 

​		`context.getBean()` 获取bean 的时候才会创建 



WebApplicationContext 环境中，另有两个作用域：

request

session 





#### bean 的生命周期

生命周期：bean 对象从创建到销毁的时间长度

1、bean对象创建（调用无参构造器）

2、给bean设置相关属性

3、bean 后置处理器

4、对bean 对象进行初始化（调用指定的初始化方法）

5、后置处理器

6、创建完成，可以使用

7、销毁（配置销毁的方法）

8、IoC 容器关闭









