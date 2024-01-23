# 简介
可扩展的标记性语言  
xml文件中的标签并不是html 这个语言定义好的, 而是自己自定义的  


是一种强语法, 如果打错了, 是不会自动调整识别的

作用: 
1. 用来**保存数据**, 同时这个数据具有描述性  
Student[id=1,name="123"]   
Student[id=2,name="name"]   

可以使用xml 文件来保存  
students.xml   
<students> 
        <student>
            <id>1</id>
            <name>123</name>
        </student>
            <id>2</id>
            <name>name</name>
        </student>
</students>

2. 可以用于项目的**配置文件**  
3. 可以作为网络传输数据的格式(现在主要使用的是JSON)  


# 语法
## 文档声明 
```
<?xml version="1.0" encoding="utf-8" ?>
<!--浏览器也可以校验-->
<!--
version="1.0" 表示xml的版本
encoding 表示xml 文件的编码
-->
<books><!--books 表示多个图书信息-->
    <book sn="SN1234567"> <!--book 表示一本图书的信息-->
        <name>java入门</name> <!--书名-->
        <author>未知</author><!--作者-->
        <price>123</price><!--价格-->
    </book>
    <book sn="SN12341234567"> <!--book 表示一本图书的信息-->
        <name>java入门到入土</name> <!--书名-->
        <author>???</author><!--作者-->
        <price>1.1</price><!--价格-->
    </book>
</books>
```
## 注释语法
与html 一样   

## 元素(标签)
可以有子元素   
也可以有属性   
### 标签名的规则  
1. 可以含字母,数字,和其他字符 
2. 名称不能有空格   
3. 标签有单标签和双标签 
    双标签中的文本, 可以放入单标签中的属性值

## 属性  
提供元素的额外信息
属性值必须使用引号引起来  

## 其他语法规则 
1. 所有的xml元素必须闭合, 如果不闭合就会报错  
2. 对大小写是敏感的
3. 标签必须正确地嵌套  
    不能互相包含
4. 文档必须有根元素   
    根元素:　就是顶级元素--->没有父标签的元素
    根元素标签是没有父标签的顶元素, 而且是**唯一的**

5. xml 中的特殊字符, 需要进行转化(换成&....)
如果有大量的特殊字符: 
    CDATA语法, 可以告诉xml 的解析器, 在CDATA里的内容，只是存文本, 不需要语法解析
    格式: 
        <![CDATA[放入不需要解析的内容]]>  

# xml的解析技术  
将xml文件文本转化成我们需要的内容   
与html 都是标记型文档, 可以使用dom来解析  
都会有个document对象, 表示整个文档对象, 树型结构    
早期JDK有两种xml解析技术: DOM 和Sax(已经淘汰)  

有其他第三方的解析  

## Dom4j解析  
docs 是文档，找index.html, 里面最重要的是Quick Start 使用这个Dom4j  
lib 需要的jar包   
src 是源码  

步骤： 
1. 在模块目录中添加一个lib目录，将dom4j 的jar包放在这个目录下(@Test 模块需要加载一个jar包， 可以将这个jar放入到lib中， 也将其添加(Add as library), 这个时候就能用Test了)
2. 使用`SAXReader reader = new SAXReader();` 该语句创建一个新的SAXReader对象
3. 通过SAXReader对象, 可以获取整个页面的Document对象 
4. 之后通过Document对象， 继续获取根元素（根标签）
5. 然后，根据根元素继续获取里面的各个子元素 

获取到的元素, 是一种Element 对象


可以使用的方法： 
- Element对象.asXML() 可以将Element 对象转化成一个XML 字符串进行显示  
- Element对象.element("") 可以通过标签名获取子元素的Element对象
- Element对象.getText()    可以获取标签之间的文本
- Element对象.elementText("")  可以根据标签名直接获取子元素标签之间的文本   
- Element对象.attributeValue("属性名")      可以根据属性名获取这个标签中指定属性的值
- 