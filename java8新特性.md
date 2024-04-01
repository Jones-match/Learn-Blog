# Lambda（闭包）

允许函数作为一个方法的参数

把函数作为一个参数传入到一个方法中



(parameters) -> expression

或

(parameters) -> { statements; }



expression 和 statements 是Lambda表达式的主体

如果只有一个参数，可以省略括号

如果没有参数，需要写空括号



## 可选类型声明

```java
//没有声明类型
Collection.sort(names, (s1, s2) -> s1.compareTo(s2));

//声明类型
Collection.sort(names, (String s1, String s2) -> s1.compareTo(s2));

```



## 可选参数圆括号

当方法只有一个参数时，不需要定义圆括号



## 可选大括号

当主体只有一行时，可以不使用大括号



## 可选的返回关键字return

如果只有一行，可以不用return，返回值的类型可由编译器自动推理



## 变量作用域

Lambda表达式可以引用类成员和局部变量，但这些变量隐式转换成final 



```java
int num = 1;
Arrays,asList(1, 2, 3, 5).forEach(e -> System.out.println(num + e));

//在Lambda表达式中调用了num 之后，就不可以再更改了
num = 2; // 错误
```



在Lambda表达式中不允许声明一个与局部变量同名的参数或局部变量

```java
int num = 1;
Arrays.asList(1, 2, 3, 4).forEach(num -> System.out.println(num)); 
//这里表达式中的num 与外部定义的局部变量num 重名，报错
```





# 函数式接口

接口： 有且仅有一个抽象方法，可以有多个非抽象方法

--->  可隐式得转为Lambda表达式

使用注解@FunctionalInterface

```java
@FunctionalInterface
public interface GreetingService {

    void sayMessage(String message);
}


GreetingService greetService = message -> System.out.println("Hello " + message);
greetService.sayMessage("world");
```



# 方法引用::

通过方法的名字来指向一个方法

有四种不同方法的引用



list.forEach(Car::run) 相当于调用list中的每个car的run方法

等价于

```java
for (Car car : list) {
    car.run();
}
```



列表.forEach(Class::method) 就是依次调用列表中的元素，并执行Class.method()方法，如果是一个静态方法，就是把每个元素当作参数传入到方法中--Class.method(元素)

如果不是静态方法，就是



## 构造器引用 

Class::new 或 Class<T>::new 

```java 
Supplier<Car> c = Car::new;
Car car = c.get();  //调用构造器，生成一个实例
```



或者是：

```java
class Car {
    public static Car create(final Supplier<Car> supplier) {
        return supplier.get();
    }
}


Car car = Car.create(Car::new);
```





## 静态方法引用

Class::static_method



静态方法中，参数必须是当前类，而且必须有这个参数，不然会报错





## 成员方法引用

Class::method



参数列表中不能有参数，否则会报错



## 实例对象的成员方法的引用

instance::method

调用一个实例对象instance的某一个方法



只接受一个Car 类型的参数





# Stream

将处理的元素看作是一种流，流在管道中传输

在传输的过程中，可以在管道中的特定节点上进行处理（过滤，排序，聚合等）

```text
| stream of elements +-----> |filter+-> |sorted+-> |map+-> |collect|
```



```java
List<Integer> list = Arrays.asList(1, 3, 4, 2, 4, 5);

List<Integer> after = list.stream()
    .filter(x -> x > 2)
    .sorted((x, y) -> x.compareTo(y))
    .map(i -> i * i)
    .distinct()
    .collect(Collectors.toList());
```



## filter 

过滤元素



例：过滤出空字符串

```java
strs.stream().filter(s -> s != "") 或 filter(s -> !s.isEmpty())
    .collect(Collectors.toList());
```

最后需要使用collect 进行收集



## limit

获取指定数量元素的流



例：打印出10条数据

```java
Random random = new Random();
random.ints().limit(10).forEach(System.out::println);
```



## sorted

对流进行排序



sorted((a, b) -> a.compareTo(b))  升序（也是默认的排序，可以不用写）

sorted((a, b) -> b.compareTo(a)) 降序





## map

映射每个元素到对应的结果



例：输出每个元素的平方数

```java
list.stream().map(i -> i * i).collect(Collectors.toList());
```



## distinct

去重



## forEach

输出流中的每个元素



## Collectors

归约操作



将流转换成集合 和 聚合元素

可用于返回列表或字符串

列表： Collectors.toList()

字符串：Collectors.joining(",")



## 统计

主要用于基本类型上

sta = summaryStatistics()

sta.getMax()

sta.getMin()

sta.getSum()

sta.getAverage()





可以避免空指针

```java
int sum = list.stream().mapToInt(o -> Objects.isNull(o.getAge()) ? 0 : o.getAge()).sum();
```





## 并行

stream().parallelStream().filter()....



并行处理程序















# Supplier 接口









