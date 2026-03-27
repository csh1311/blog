---
title: JAVA基础
date: 2022-12-16
tags:
toc: true
published: false
---

java之父---高斯林

Java的发展可以分为以下几个阶段：

1. 1995年：Java语言的诞生。
2. 1996年：Java 1.0版本的发布。
3. 1997年：Java 1.1版本的发布，新增了事件处理模型等功能。
4. 1999年：Java 2 Platform Standard Edition 1.2版本的发布，支持动态Web内容。
5. 2002年：Java 2 Platform Standard Edition 1.4版本的发布，引入了注解、NIO等新特性。
6. 2004年：Java 5.0版本的发布，引入了泛型、可枚举类型等特性。
7. 2006年：Java 6版本的发布，改进了XML处理、并行计算等方面。
8. 2011年：Java 7版本的发布，增加了语言级别的支持。
9. 2014年：Java 8版本的发布，引入了Lambda表达式、Streams API等新特性。
10. 2018年：Java 10版本的发布，带来了更多的语言和性能改进。

1. JDK是什么？有哪些内容组成？

   ​           JDK是java开发工具包

   - ​	JVM虚拟机：java程序运行的地方
   -    核心类库：java已经写好的东西，我们可以直接用。
   -    开发工具：javac、java、jdb、jhat

2. JRE是什么？有哪些内容组成？

   JRE是java运行环境

   JVM、核心类库、运行工具

3. JDk、JRE、JVM三者包含关系

   - JDK包含JRE
   - JRE包含JVM



#### 重点

- 在ACIIL表中字符'1'对应的数字是49，字符'0'对应的字符是48，这两个字符'1'-'0'等于数字1



#### 算术运算符

隐式转换小结

1. 取值范围

   byte<short<int<long<float<double

2. 什么时候转换

   数据类型不一样，不能计算，需要转成一样的数据类型才可以计算

3. 转换规则1：

   取值范围小的，和取值范围大的进行运算，小的会先提升为大的，再进行运算

4. 转换规则2

   byte short char 三种类型的数据在运算的时候，都会直接先提升到int，然后再进行运算

![image-20220919165559479](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220919165559479.png)





#### 数组

- 数组定义

  - 数据类型[]   数组名 =  new 数据类型[]{元素1，元素2，元素3}
  - 数据类型[]  数组名 = {}

  例：

  ```java
  //        定义数组存储5个学生年龄
          int[] arr = {15,17,16,13};
          int[] ar1 = new int[]{15,17,16,13};
          System.out.println(arr);  //[I@1b6d3586
          System.out.println(ar1);  //[I@4554617c
  
          //扩展
          //解释数组的地址值  //[I@1b6d3586
          //[ : 表示当前是一个数组
          //I ： 表示当前数组里面的元素都是int类型
          //@ ： 表示一个间隔符。固定格式
          //1b6d3586：才是数组真正的地址。（十六进制）
          //平时会把整个叫做数组地址值
  ```

- java内存分配

  - java运行是虚拟机也会占用内存，但是为了更好的利用这块内存，虚拟机又分配了5个部分，每个部分都有它自己的作用

  ​     <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902133323410.png" alt="image-20220902133323410" style="zoom:67%;" />

  - jdk7以前方法区和堆是连在一起的

  <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902162900225.png" alt="image-20220902162900225" style="zoom:67%;" />

  - 注意：从jdk8开始取消了方法区，新增了元空间。把原来方法区的多种功能进行拆分，有的功能放在队中有的功能放在元空间中

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902163809082.png" alt="image-20220902163809082" style="zoom:67%;" />

- 
  - 栈   方法运行使用的内存，比如main方法运行，进入栈内存中
  - 堆   存储对象或数组，只要new来创建的都进入堆内存中
  - 方法区   存储可以运行class文件
  - 本地方法栈   jvm使用操作系统的功能是使用，与开发无关
  - 寄存器  给cpu使用，与开发无关

- 数组内存分配

  - 只要是new出来的一定是在堆里面开辟一个小空间

  - 如歌new了多次，那么堆里就有多少个小空间，而且每个小空间都有各自的数据

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902165249568.png" alt="image-20220902165249568" style="zoom:67%;" />

  - 当两个数组指向同一个空间的，其中一个数组对空间数据中的值发生改变，那么其他数据再次访问的时候都是修改之后的结果

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902165249568.png" alt="image-20220902165249568" style="zoom:67%;" />

#### 方法

- 什么是方法

  方法是程序中最小的执行单元

  1. 实际开发中，什么时候用到方法？

     ​	重复的代码，具有独立功能的代码可以抽到方法中

  2. 实际开发中，方法有什么好处

  ​            提高代码的复用性

  ​			提高代码的维护

- 方法的格式

  - 最简单的方法定义

    - 方法的定义

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902171840717.png" alt="image-20220902171840717" style="zoom:67%;" />

    - 方法的调用

      ![image-20220902172119284](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902172119284.png)

      ```java
      package Day;
      
      public class Day04 {
          public static void main(String[] args) {
              //方法的调用
              playGame();
              /**
               * 练习
               *定义一个方法，在方法中定义两个变量进行求和
               */
              sum();
          }
      
          /**
           * 注意：定义方法是在main主方法外面，但是方法的调用在主方法里面
           */
          //定义一个方法
          public static void playGame(){
              System.out.println("准备");
              System.out.println("确定");
              System.out.println("操作");
              System.out.println("结束");
          }
      
          //定义一个求和的方法
          public  static  void sum(){
              int a = 10;
              int b = 20;
              int result = a+b;
              System.out.println(result);
          }
      }
      
      ```

      

  - 带参数的方法定义

    - 带参数方法的定义

      ![image-20220902210944199](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902210944199.png)

    - 带参数方法发调用

      ![image-20220902211057405](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902211057405.png)

    ```
    
    ```

    - 形参和实参

      - 形参：全称形式参数，是指方法定义中的参数

      - 实参：全称实际参数，是指调用的参数

        ![image-20220902211724508](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902211724508.png)

      ```
          public static void main(String[] args) {
              //调用求长方形的周长，将结果在方法中进行
              rectangle(5.5,6.5);
      
              //调用求圆的面积，将结果在方法中打印
              circle(4.0);
          }
          
              //定义一个长方形周长方法
          public static void rectangle(double len,double width){
              double result = (len+width)*2;
              System.out.println(result);
          }
      
          //定义一个求圆的面积
          public static void circle(double r){
              double S = 3.14*(r*r);
              System.out.println(S);
          }
      
      ```

      

  - 带返回值的方法定义

    - 带返回值方法的定义

      ![image-20220902220113515](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220902220113515.png)

    - 带返回值方法的调用

    ```
        public static void main(String[] args) {
            //调用长方形面积
            double are = getAre(3.0, 4.0);
            double are1 = getAre(4.0, 3.0);
            if (are > are1){
                System.out.println("第一个长方形面积大于第二个长方形面积");
            }else {
                System.out.println("第二个长方形面积大于第一个长方形面积");
            }
    
        }
        
        
        //定义一个求长方形面积的方法
        public  static double getAre(double len,double width){
            double res = len*width;
            return res;
        }
    ```

    - 方法的注意事项
      - 方法不调用就不执行
      - 方法与方法之间是平级关系，不能互相嵌套
      - 方法的编写顺序和执行顺序无关，根据方法调用顺序有关
      - 方法的返回值类型为void，表示该方法没有返回值，没有返回值的方法可以省略return语句不写。如果要编写编写return，后面不能跟具体的数据。
      - return语句下面，不能编写代码，因为永远执行不到，属于无效代码
    - return关键字
      - 方法没有返回值：可以省略不写。如果书写，表示结束方法
      - 方法有返回值：必须要写。表示结束方法和返回结果是

- 方法的重载

  - 什么是方法的重载

    - 在同一个类中，定义了多个同名的方法，这些同名的方法具有同种的功能
    - 每个方法具有不同的参数类型或参数个数，这些同名的方法，就构成了重载关系

    简单机：同一个类中，方法名相同参数不同的方法。与返回值无关

    ​				参数不同：个数不同、类型不同、顺序不同

- 方法的内存

  - 方法调用的基本内存原理
  - 方法传递基本数据类型原理
    - 基本数据类型：变量存储的都是真是数据
      - 整数类型
      - 浮点数类型
      - 布尔类型
      - 字符类型
    - 引用数据类型：在栈内记录的是地址值，使用其他空间的数据
      - 除了上面基本数据类型都是
  - 方法传递引用数据类型的内存原理

#### 面向对象

- 设计对象并使用

  - 类和对象： 必须先设计类才能获取对象

    - 类（设计图）:是对象共同特征的描述
    - 对象：是真实存在的具体东西

  - 类的几个注意事项

    - 用来描述一类事物的类，专业叫做：javabean类。在javabean类中，是不写mian方法的。
    - 在以前。编写mian方法的类，叫做测试类。我们可以在测试类中创建Javabean类对象并进行赋值调用。

  - 总结

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220904100155619.png" alt="image-20220904100155619" style="zoom:67%;" />

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220904100217142.png" alt="image-20220904100217142" style="zoom:67%;" />

- 封装

  - 

- this关键字

  - 可以区别成员变量和局部变量

- 构造方法

  - 作用：
    - 创建对象的时候，由虚拟机自动调用，给成员变量进行初始化的。
  - 特点：
    - 方法名与类名相同，大小写也要一致
    - 没有返回值类型，连void都没有
    - 没有具体的返回值（不能由retrun带回结果的数据）
  - 构造方法有几种，各自的作用是什么。
    - 无参数构造方法：初始化对象是，成员变量的数据均采用默认值。
    - 有参数构造方法：在初始对象时候，同时可以为对象进行赋值。
  - 执行时机
    - 创建对象的时候由虚拟机调用，不能手动调用构造方法
    - 每创建一次对象，就会调用一次构造方法
  - 构造方法定义
    - 如果没有定义构造方法，系统将给出一个默认的无参数构造方法
    - 如果定义构造方法，系统将不再提供默认的构造方法
  - 构造方法的重载
    - 带参构造方法，和无参构造方法，两者方法名相同但是参数不同，这叫做构造方法的重载
  - 推荐的使用方式
    - 无论是否使用，都手动书写无参数构造的方法，和带全部参数的构造方法
  - 构造方法有哪些注意事项
    - 任何类定义出来，默认自带了无参数构造器，写不写都有。
    - 一旦定义了有参数构造器，无参数构造器就没有了，此时就需要自己写无参数构造器了。
    - 建议在任何时候都手动写上空参和带全部参数的构造方法

- 标准javaBean

  - 类名需要见名知意
  - 成员变量使用private修饰
  - 提供至少两个构造方法、
    - 无参构造方法
    - 有参构造方法
  - 成员方法
    - 提供每一个成员变量对应的setXxx()/getXxx()
    - 如果还要其他行为，也需要写上

- 对象内存图

  - 一个对象的内存图

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220904110844634.png" alt="image-20220904110844634" style="zoom: 50%;" />

  - 多个对象的内存图

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220904111831605.png" alt="image-20220904111831605" style="zoom: 50%;" />

  - 两个引用指向同一个对象的内存图

    <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220904111856074.png" alt="image-20220904111856074" style="zoom:50%;" />

  - this的内存图原理

    - this的作用:区分局部变量和成员变量
    - this的本质：所在方法调用者的地址值

  - 基本数据类型和引用数据类型的区别

  - 局部变量和成员变量的区别

- 补充知识：成员变量、局部变量区别

  - 成员变量：类中方法外的变量
  - 局部变量：类中方法内的变量

  ![image-20220904162404297](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220904162404297.png)

- 修饰符

  - private
    - 是一个权限修饰符
    - 可以修饰成员（成员变量和成员方法）
    - 被private修饰的成员只能在本类中才能访问

练习

```java
package Day.dayMxdx;

/**
 * 定义一个长度为3的数组，数组存储1~3名学生对象作为初始化数据，学生对象的学号，姓名各不相同。
 * 学生属性：学号，姓名，年龄
 * 要求1：再次添加一个学生对象，并在添加的时候进行学号的唯一判断
 * 要求二：添加完毕之后遍历所有学生信息
 * 要求三：通过id删除，如果不存在，则提示删除失败
 * 要求四：删除后遍历所有学生信息
 * 要求五：查询数组id为“heima002”的学生，如果存在，则将他年龄+1；
 */
public class Student {

    private String id;
    private String name;
    private int age;

    public Student() {
    }

    public Student(String id, String name, int age) {
        this.id = id;
        this.name = name;
        this.age = age;
    }

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

//测试类

package Day.dayMxdx;

/**
 * 定义一个长度为3的数组，数组存储1~3名学生对象作为初始化数据，学生对象的学号，姓名各不相同。
 * 学生属性：学号，姓名，年龄
 * 要求1：再次添加一个学生对象，并在添加的时候进行学号的唯一判断
 * 要求二：添加完毕之后遍历所有学生信息
 * 要求三：通过id删除，如果不存在，则提示删除失败
 * 要求四：删除后遍历所有学生信息
 * 要求五：查询数组id为“heima002”的学生，如果存在，则将他年龄+1；
 */



public class StudentTest {
    public static void main(String[] args) {
        //定义一个长度为3的数组
        Student[] arr = new  Student[3];

        //定义对象
        Student s1 = new Student("001","小明",18);
        Student s2 = new Student("002","小东",20);
        Student s3 = new Student("003","小蔡",22);
        //数组存储1~3名学生对象作为初始化数据
        arr[0] = s1;
        arr[1] = s2;
        arr[2] = s3;

        //再次添加一个对象到数组里面
        Student s4 = new Student("004","小第",28);
//        调用判断方法
        Boolean flag = repetition(arr, s4.getId());
        if (flag){
            System.out.println("数组里面已经存在id，请重新跟换id在添加");
        }else {
            int count = getCount(arr);
            //如果相等则数组长度不够
            if (count==arr.length){
                //重新创建数组
                Student[] createArr = createArr(arr);
                createArr[count] = s4;
                for (int i = 0; i < createArr.length; i++) {
                    Student student = createArr[i];
                    System.out.println(student.getId()+","+student.getName()+","+student.getAge());
                }
            }else {
                arr[count] = s4;
            }
        }
        //根据id删除
        int index = getId(arr, "002");
        if (index == -1) {
            System.out.println("数组没有这个id，删除失败");
        }else{
            Student[] students = deleteArray(arr,index);
            System.out.println("删除成功");
            for (int i = 0; i < students.length; i++) {
                Student student = students[i];
                System.out.println(student.getId()+","+student.getName()+","+student.getAge());
            }
        }
        //查询数组id为“heima002”的学生，如果存在，则将他年龄+1
        //根据id删除
        int indexs = getId(arr, "003");
        if (indexs == -1) {
            System.out.println("数组没有这个id");
        }else{
            Student student = arr[indexs];
            System.out.println(student.getId()+","+student.getName()+","+(student.getAge()+1));
        }

    }
    //定义一个方法判断数组数据
    public static  int getCount(Student[] arr){
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
            if (arr[i]!=null){
                count++;
            }
        }
        return count;
    }

    //定义一个方法，判断数组里面是否有重复的数据
    public static Boolean  repetition(Student[] arr, String id){
        for (int i = 0; i < arr.length; i++) {
            Student student = arr[i];
            if (student.getId()==id){
                return true;
            }
        }
        return  false;
    }
    
    //定义一个如果数组长度不够，重新创建数组，然后数组长度等于旧数组的长度+1
    public static  Student[]  createArr(Student[] arr){
        Student[] createArr = new Student[arr.length+1];
        for (int i = 0; i < arr.length; i++) {
            createArr[i] = arr[i];
        }
        return createArr;
    }

    //定义一个方法根据id查询出索引的位置
    public  static  int getId(Student[] arr, String id){
        int count = -1;
        for (int i = 0; i < arr.length; i++) {
            Student s = arr[i];
            if (s.getId()==id){
                count = i;
                break;
            }
        }
        return count;
    }

    //定义一个方法删除数组元素
    public static  Student[] deleteArray(Student[] arr,int index){
        Student[] newArray = new  Student[arr.length-1];
        for (int i = 0; i < newArray.length; i++) {
            if (index<0 || index > arr.length){
                System.out.println("数组越界");
            }
            if (i<index){
                newArray[i] = arr[i];
            }else {
                newArray[i] = arr[i+1];
            }
        }
        System.out.println(newArray.length);
        return  newArray;
    }
}


```

#### API和API文档

- API文档：应用程序编程接口

  - 简单理解：API就是别人已经写好的东西，我们不需要自己编写，直接使用即可

- Java API：指的就是JDK中提供的各种功能的java类，这些类将底层的实现封装了起来，我们不需要关心这些类是如何实现的，只需要学习这些类如何使用即可。

- String

  - 字符串的内容是不会发生改变的，它的对象创建后不能被更改

  - 创建String对象的两种方式

    ![image-20220907145255890](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220907145255890.png)

  - String内存模型

    - 当使用双引号直接赋值时，系统会检查该字符串在串池中是否存在。

      - 不存在：创新的
      - 存在：复用

      ![image-20220907145634099](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220907145634099.png)

    - 当使用new创建赋值是

      - 每new一个就会在堆里面创建小空间，不会使用Strin Table(串池)，这样会大量的使用内存

      ![image-20220907145839923](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220907145839923.png)

    - 字符串之间比较

      - 第一个方式创建和第二个方式new出来的用==于比较是等于false，因为它们比较的是地址值

        ```java
        String name = "dasdadas";    //进入内存的串池
        String names =  "dasdadas";
         System.out.println(name==names);  //true
        
         String n = new String("dasdadas");   //直接在堆空间中生成小空间
                System.out.println(name==n);  //false
        
        
        
               //字符串比较
                boolean equals = n.equals(name);
                System.out.println("equals:"+equals);   //true
                boolean equal = n.equals(names);
                System.out.println("equal:"+equal);   //true
        
                //字符串忽略大小写比较
                String s = new String("Abc");
                String s1 = "abc";
                boolean b = s.equalsIgnoreCase(s1);
                System.out.println(b);   //true
        ```

      - Boolean equals 方法（要比较的字符串）                  完全一样结果是true，否则为false

      - Boolean equalslgnoreCase（要比较的字符串）       忽略大小写的比较

  - StringBuilder

    - 可以看成是一个容器，创建之后内容是可以改变的

    - StringBuilder常用方法

      ![image-20220907231629383](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220907231629383.png)

    - 使用StringBuilder的场景

      - 字符串拼接
      - 字符串的反转

  - StringJoiner

    - StringJoiner跟StringBuilder一样，也可以看成是一个容器，创建之后里面的内容是可变的
    - 作用：提高字符串的操作效率，而且代码编写特别简洁，但是目前市场上很少有人用
    - JDK8才出现的

  - 字符串原理

    - ==号比较的到底是什么？
      - 基本数据类型比较数组值
      - 引用数据类型比较地址值

  - 字符串拼接的底层原理

    - 如果很多字符串变量拼接，不要直接+。在底层会创建多个对象，浪费时间，浪费性能。
    - 如果没有变量参与，都是字符串直接相加，编译之后就是拼接之后的结果，会复用串池中的字符串
    - 如果有变量参与，每一行拼接的代码，都会在内存中创建新的字符串，浪费内存

  - StringBuilder底层原理

    - 所有要拼接的内容都会往StringBuilder中放，不会创建很多无用的空间，节约内存
    
  - ArrayList集合

    - 长度可以变
    - 集合不能直接存储基本数据类型

  - static（静态）

    - static表示静态，是java中的修饰符，可以修饰成员方法，成员变量
    - 被static修饰的成员变量，叫做静态变量
      - 特点：
        - 被该类所有对象共享
        - 不属于对象，属于类
        - 随着类的加载而加载，优先于对象存在
      - 调用方法：
        - 类名调用
        - 对象名调用
    - 被static修饰的成员方法，叫做静态方法
      - 特点
        - 多用在测试类和工具类
        - javabean类中很少会用

      - 调用方法
        - 类名调用
        - 对象名调用
    - 工具类
      - 类名见名之义
      - 私有化构造方法
      - 方法都定义为静态方法，方便调用
    - static的注意事项
      - 静态方法只能访问静态变量和静态方法
      - 非静态方法可以访问静态变量或者静态方法，也可以访问非静态的成员变量和静态的成员方法
      - 静态方法中是没有this关键字
    - 总结：
      - 静态方法中，只能访问静态。
      - 非静态方法可以访问所有。
      - 静态方法中没有this关键字

#### 继承

- java中提供一个关键字extedns

- 当类与类之间，存在相同（共性）的内容，并满足子类是父类中的一种，就可以考虑使用继承，来优化代码

- 什么是继承、继承的好处？

  - 继承是面向对象的三大特征之一，可以让类跟类之间产生子父的关系
  - 可以把多个子类中重复的代码抽取到父类中，子类可以使用，减少代码冗余，提高代码的复用性

- 继承的格式？

  - public class 子类 extedns 父类 {}

- 继承后子类的特点？

  - 子类可以得到父类的属性和行为，子类可以使用。
  - 子类可以在父类的基础上新增其他功能子类更强大

- 子类到底能继承父类中的哪些内容？（内存图/内存分析工具）

  <img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220911173759076.png" alt="image-20220911173759076" style="zoom:50%;" />

- 继承的特点

  - java只支持单继承，不支持多继承，但支持多层继承。
    - 一个子类只能继承一个父类，子类不能同时继承多个父类，子类A继承父类B，父类B可以继承父类C。

- 继承中：成员变量的访问特点

  - 就近原则：谁离我近，我就用随

    - 先在局部位置找，本类成员位置找，父类成员位置找，逐级往上

  - 如歌出现了重名的成员变量怎么办吗？

    ```java
    System.out.println(name);
    System.out.println(this.name); 
    System.out.println(super.name); //去找父类的name
    ```
    
    

- 继承中：成员方法的访问特点

- 继承中：构造方法的访问特点

  - 父类中的构造方法不会被子类继承，但是可以通过super来调用
  - 子类构造方法的第一行，有一个默认的super();
  - 默认先访问父类中无参的构造方法，在执行自己
  - 如果想要方法文父类有参构造方法，必须手动书写。
  - 子类中所有的构造方法默认先访问父类中的无参构造，在执行自己

#### 重写

- 方法的重写
  - 当父类的方法不能满足子类现在的需求时，需要进行方法的重写
  - 重写方法的名称、形参列表必须与父类一致
  - 子类重写父类方法时，访问权限子类必须大于等于父类（暂时了解：空着不写<protected<public)
  - 子类重写父类的方法时，返回值类型子类必须小于父类
  - 只有被添加到虚方法表中的方法才能被重写
- 书写格式
  - 在继承体系中，子类出现了和父类中一模一样的方法声明，我们称子类这个方法是重写的方法
- @Override重写的注解
  - @Override是放在重写后的方法上，校验子类重写是语法是否正确
  - 加上注解后如果有红色波浪线，表示语法错误
  - 建议重写方法都加上@Override注解，代码安全，优雅

#### this，super()

- this:理解为一个变量，表示当前方法调用者的地址值；
- super:代表父类存储空间。

#### ![image-20220912094526173](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220912094526173.png)多态

- ​	什么是多态？
  - 同类型的对象，表现出的不同的形态

- ​	多态的表现形式
  - 父类类型 对象名称 = 子类对象；

- 多态的前提
  - 有继承关系
  - 有父类引用指向子类对象
  - 有方法重写
- 多态的好处？
  - 使用父类型作为参数，可以接收所有子类对象，体现多态的扩展性与便利
- 多态调用成员的特点
  - 变量调用:编译看左边，运行看右边。
  - 方法调用：编译看左边，运行看右边。
- 多态的优势
  - 方法中，使用父类型作为参数，可以接受所有子类对象
- 多态的弊端是什么？
  - 不能使用子类的特有功能
- 引用数据类型的类型转换，有几种方式？
  - 自动类型转换，强制类型转换
- 强制类型转换能解决什么问题？
  - 可以转换成真正的子类型类型，从而调用子类独有功能
  - 转换类型与真实对象类型不一致会报错
  - 转换的时候用instanceof关键字进行判断

#### final 

​	使用final修饰之后是不能改变的

- 方法 表面该方法最终方法，不能被重写
- 类instanceof表面该类是最终类，不能被继承
- 变量 叫做常量，只能被赋值一次
- final修饰变量：是常量，不能修改
  - 基本数据类型：变量的值不能修改
  - 引用数据类型：地址值不能修改但是内部的属性值可以修改

使用场景

- ​	一些系统不可被修改的常量

#### 权限修饰符

- private ： 私有的，只能 自己用

- 默认 ： 只能在本包里面用

- protected ： 受保护的

- public ： 公共的

  ![image-20220912153212668](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220912153212668.png)

1. 构造代码块
   1. 写在成员位置的代码块
   2. 作用：可以把多个构造方法中重复的代码抽取出来
   3. 执行时机：我们在创建本类对象的时候会执行构造代码块再执行构造方法
2. 静态代码块
   1. 格式：static{}
   2. 数据的初始化（重点）
   3. 执行时机：随着类的加载而加载的，并且只执行一次

#### 抽象类

- 抽象类
  - public abstract class 类名{}
  - 如果一个<u>类中存在抽象方法</u>，那么这个类就<u>必须声明为抽象类</u>
- 抽象方法
  - 格式:public abstract 返回值类型 方法名（参数列表）；
  - 抽象方法：将共性的行为（方法）抽取到父类之后。由于每一个子类执行的内容不一样，所以，再父类中不能确定具体的方法体。该方法就可以定义为抽象方法。
- 子类继承抽象类之后，如何重写抽象方法
- 抽象类和抽象方法注意事项
  - 抽象类不能实例化（抽象类不能创建对象）
  - 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类
  - 可以有构造方法
  - 抽象的子类
    - 要么重写抽象类中的所有抽象方法
    - 要么是抽象类
- 抽象类的作用是声明样的？
  - 抽取共性时，无法确定方法体，就把方法定义为抽象的，强制让子类按照某种格式重写。

#### 接口

- 接口：就是一种规则
- 接口的定义和使用
  - 接口用关键字interface来定义
    - public interface 接口名{}
  - 接口不能实例化
  - 接口和类之间是实现关系，通过implements关键字表示
    - public class 类名implement 接口名 {}
  - 接口的子类（实现类）
    - 要么重写接口中的所有抽象方法
    - 要么是抽象类
- 接口成员的特点
  - 成员变量
    - 只能是常量
    - 默认修饰符：public static final
  - 没有构造方法
  - 成员方法
    - 只能是抽象方法
    - 默认修饰符：public abstract
  - jdk7以前：接口只能定义抽象方法
- 接口和类之间的关系
  - 类和类之间的关系
    - 继承关系，只能单继承，不能多继承，但是可以多层继承
  - 类和接口的关系
    - 实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现多个接口
  - 接口和接口的关系
    - 继承关系，可以单继承，也可以多继承

#### 内部类

- 类的五大成员：

  - 属性，方法，构造方法、代码块、内部类

- 内部类的分类

  - 成员内部类

    - 写在成员位置，属于外部类的一员

    - 成员内部类可以被修饰符所修饰

    - 在成员内部类里面，JDK16之前不能定义静态变量，JDK16才开始可以定义静态变量

    - 调用格式

      ```
      package Day;
      
      public class Day06Test {
      
      
          public static void main(String[] args) {
              
      //        创建内部类对象
              Day06.Engine  e= new Day06().new Engine();
              e.show();
              //创建内部类对象,在外部类创建一个成员方法来调用内部类的对象
              Day06 d = new Day06();
              Day06.Engine engine = d.getEngine();
              engine.show();
          }
      
      
      }
      ```

      

  - 静态内部类

    ![image-20220914224011897](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220914224011897.png)

  - 局部内部类

    - 将内部类定义在方法里面就叫做局部内部类，类似于方法的局部变量
    - 外界是无法直接使用，需要在方法内部创建对象并使用
    - 该类可以直接访问外部类的成员，也可以访问方法内的局部变量

  - 匿名内部类

    - 内部类本质上就是隐藏了名字的内部类
    - 定义格式

    ```
    new 类名或者接口名(){      //如歌类名是类那么就是继承关系，如果是接口名那么就是实现接口
    	重写方法;
    };
    ```

    

- 什么是内部类

  - 在一个类中，再定义一个类

- 内部类的访问特点

  - 内部类可以直接访问外部类的成员，包括私有

  - 外部类要访问内部类的成员，必须创建对象

    ```
    package Day;
    
    public class Day06 {
        String carName;
        int carAGe;
        String carColor;
     	int a = 30;
    
        //定义一个外部类的方法
        public  void  shows(){
            //外部类访问成员变量
            System.out.println(carAGe);
            //外部类访问不了内部类的成员变量
    //        System.out.println(engineAgge);
            //外部类访问不了内部类的成员方法
    //        show();
    
        }
    
        //定义一个内部类
        class Engine{
            String engineName;
            int engineAgge;
            int a = 10;
    
            //定义一个内部类的方法
            public void show(){
             	int a = 20;
                //内部类访问内部类的成员变量
                System.out.println(engineName);
                //内部类访问外部类的成员变量
                System.out.println(carName);
                //内部类访问外部类的成员方法
                shows();
                //如果内部类和外部类的成员变量同名需要以下方法调用
                 System.out.println(a);//20
                 System.out.println(this.a);  //10
                 System.out.println(Day06.this.a);//30
            }
        }
    
    }
    ```

#### Math

```
package math;

public class MathTest {
    public static void main(String[] args) {
        float a = 314554.88f;
        int round = Math.round(a);
        System.out.println(round);


        //返回绝对值
        int b = -100;
        int abs = Math.abs(b);
        System.out.println(abs);

        //返回两个数的总数 如果数据超出int范围会抛出异常
        int x = 2, y = 10;
        int i = Math.addExact(x, y);
        System.out.println(i);
        //返回乘数的乘积

        //比较两个数的最大值
        int maxA= 10,maxB=20;
        int max = Math.max(maxA, maxB);
        System.out.println(max);


        //比较两个数的最小值
        int minA=50,minB=60;
        int min = Math.min(minA, minB);
        System.out.println(min);

        //返回两个数的相乘
        int i1 = Math.multiplyExact(x, y);
        System.out.println(i1);

        //向上取整
        System.out.println(Math.ceil(20.85));//21.0

        //向下取整
        System.out.println(Math.floor(20.85));//20.0

        //代表2的三次方，如果第二个参数是0~1之间的小数
        System.out.println(Math.pow(2, 3)); //8.0
        System.out.println(Math.pow(2, 0.5)); //1.4142135623730951

        //代表开根号
        System.out.println(Math.sqrt(98)); //2.0

        //开立方根
        System.out.println(Math.cbrt(8));//2.0


    }
}

```

#### System

<img src="https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220918172005955.png" alt="image-20220918172005955" style="zoom:67%;" />

```
package math;

public class SystemTest {
    public static void main(String[] args) {
        //0:表示当前虚拟机是正常停止
        //非0，表示当前虚拟机异常停止
//        System.exit(0);

        long l = System.currentTimeMillis();
        System.out.println(l);

        //拷贝数组
        int[] arr1 = {1,2,3,4,5,6,7,8,9,10};
        int[] arr2 = new int[10];
        //第一个参数：数据源，要拷贝的数据
        //第二个参数：从数据源哪个索引开始拷贝
        //第三个参数：新数组
        //第四个参数：拷贝到新数组的哪个位置
        //第五个参数：拷贝多少个数据
//        System.arraycopy(arr1,3,arr2,0,7);


        //课堂练习 arr2 : 0 0 0 0 1 2 3 0 0 0
        System.arraycopy(arr1,0,arr2,4,3);




        for (int i = 0; i < arr2.length; i++) {
            System.out.print(arr2[i]+" ");
        }
    }
}

```

#### Runtime

- Runtime表示当前虚拟机的运行环境

  ```
  package math;
  
  import java.io.IOException;
  
  public class RuntimeTest {
      public static void main(String[] args) {
          Runtime runtime = Runtime.getRuntime();
          System.out.println(runtime);
          int i = runtime.availableProcessors();    //获取CPU的线程数
          System.out.println(i);//12
          long l = runtime.maxMemory();   //JVM能从系统中获取总内存大小(单位byte)
          System.out.println(l);
          long l1 = runtime.totalMemory();   //JVM已经从系统中获取总内存大小(单位byte)
          System.out.println(l1);
  
          long l2 = runtime.freeMemory();   //获取jvm剩余多少内存可以使用
          System.out.println(l2);
  
          try {
             runtime.exec("notepad"); //运行cmd命令 notepad打开记事本
          } catch (IOException e) {
              throw new RuntimeException(e);
          }
  
      }
  }
  
  ```

#### Object

- Object是java中定级父类。所有类都直接或间接的继承于Object类

- Object类中的方法可以被所有子类访问。

- Object方法

  - toString
  - equals
  - clone()` 对象克隆
    - 方法在底层会帮我们创建一个对象，并把原对象中的数据拷贝过去
    - 重写Object中的clone方法
    - 让JavaBean类实现Cloneable接口
    - 创建元对象并调用clone就可以了
    - 浅克隆
    - 深克隆
      - 以下的代码深克隆还是有弊端，因为以后是个二维数组又要修改，所以会使用第三方写的代码Gson

  ```
  package math;
  
  import java.util.Arrays;
  import java.util.Objects;
  
  public class Student implements Cloneable {
      private String name;
      private int  age;
  
      private int[] arr;
  
  
      public String getName() {
          return name;
      }
  
      public void setName(String name) {
          this.name = name;
      }
  
      public int getAge() {
          return age;
      }
  
      public void setAge(int age) {
          this.age = age;
      }
  
      public int[] getArr() {
          return arr;
      }
  
      public void setArr(int[] arr) {
          this.arr = arr;
      }
  
      public Student(String name, int age, int[] arr) {
          this.name = name;
          this.age = age;
          this.arr = arr;
      }
  
      public Student() {
      }
  
      //重写object中的toString
      @Override
      public String toString() {
          return "Student{" +
                  "name='" + name + '\'' +
                  ", age=" + age +
                  ", arr=" + Arrays.toString(arr) +
                  '}';
      }
      //重写object中的equals
      @Override
      public boolean equals(Object o) {
          if (this == o) return true;
          if (o == null || getClass() != o.getClass()) return false;
          Student student = (Student) o;
          return age == student.age && Objects.equals(name, student.name) && Arrays.equals(arr, student.arr);
      }
  
      //重写object中的clone
      @Override
      protected Object clone() throws CloneNotSupportedException {
  
          //如果想深克隆,不加这个就是浅克隆。浅克隆如果是引用类型那么复制的是地址值，如果成员属性中有数组，那么复制的是地址值，
          // 如果其中一个修改数组中的元素就会跟着修改，所以定义深克隆
  
          int[] data = this.arr;
          //创建新数组，将旧数组里面的数据直接拷贝的新数组里面
          int[]  newData = new int[data.length];
          for (int i = 0; i < data.length; i++) {
              newData[i] = data[i];
          }
         //直接调用父类中的方法克隆对象
          Student s = (Student) super.clone();
          s.arr = newData;
          return s;
      }
  
  
      /**
       * 浅克隆
       */
  //    @Override
  //    protected Object clone() throws CloneNotSupportedException {
  //        return super.clone();
  //    }
  }
  
  ```

  ```
  package math;
  
  public class ObjectTest {
      public static void main(String[] args) throws CloneNotSupportedException {
  
          int[] data= {1,2,3,4,5,6,7,8,9,10};
          Student s = new Student("蔡",20,data);
          System.out.println(s);   //Student{name='蔡', age=20, arr=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]}  在javaBean中重写toString就可以这样显示
          System.out.println(s);    //math.Student@1b6d3586    如果没有重写toString方法就会打印出地址值，会使用Object的toString
  
  
          Student s1 = new Student();
          Student s2 = new Student();
          boolean result = s1.equals(s2);
          System.out.println(result);   //false  如果在javaBean中不重写equals方法就会比较两个对象的地址值两个地址值是new出来的所以在内存堆中,会使用Object的equals
  
          System.out.println(result);   //true  如果在javaBean中重写equals方法就会使用javaBean中重写的equals方法。
  
  
  
          //直接调用javabean类中重写的克隆方法
          Student s4 = (Student) s.clone();
          //修改拷贝后数组的第一个元素的数据
          int[] arr = s4.getArr();
          arr[0] = 55;
          System.out.println(s4);  //Student{name='蔡', age=20, arr=[55, 2, 3, 4, 5, 6, 7, 8, 9, 10]}
          System.out.println(s);  //原数组的数组第一个数据也被修改了Student{name='蔡', age=20, arr=[55, 2, 3, 4, 5, 6, 7, 8, 9, 10]}
  
  
          //在javabean中重写了浅克隆，变成了深克隆
          System.out.println(s4);  //Student{name='蔡', age=20, arr=[55, 2, 3, 4, 5, 6, 7, 8, 9, 10]}
          System.out.println(s);   //Student{name='蔡', age=20, arr=[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]}
  
  
      }
  }
  
  ```
  

#### BigInteger

- BigInteger构造方法

  ![image-20220919214226833](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220919214226833.png)

  

#### BigDecima

- 用于小数的精确计算

- 用来表示很大的小数

  ```
  package math;
  
  import java.math.BigDecimal;
  
  public class BigDecimalTest {
      public static void main(String[] args) {
  
          //使用double形参构造函数会数据不精确
          BigDecimal b = new BigDecimal(0.01);
          BigDecimal bg = new BigDecimal(0.09);
          BigDecimal bg1 = b.add(bg);
          System.out.println(b);  //0.01000000000000000020816681711721685132943093776702880859375
          System.out.println(bg);//0.0899999999999999966693309261245303787291049957275390625
          System.out.println(bg1);//0.09999999999999999687749774324174723005853593349456787109375
  
  
          //使用String形参构造函数数据精确
          BigDecimal b1 = new BigDecimal("0.01");
          BigDecimal b2 = new BigDecimal("0.09");
          //add b1加上b2
          BigDecimal b3 = b1.add(b2);
          System.out.println(b1);  //0.01
          System.out.println(b2);//0.09
          System.out.println(b3);//0.10
  
      }
  }
  
  ```

#### 正则表达式

- 作用

  - 检验字符串是否满足规则
  
  - 在一段文本中查找满足要求的内容

  - 正则表达式字符的基本操作
  
    ![image-20220923130744244](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220923130744244.png)
  
  ```
  package Day.Api.zhengze;
  
  public class Test {
      public static void main(String[] args) {
          //判断一个是不是qq号
          String qq = "1311871826";
          //[1-9]这个代表上面第一个数字不能以0开头  \\d代表数字 {4,9}这个代表除了第一个数字后面的数必须是4~9位数字要不然就是返回false
          System.out.println(qq.matches("[1-9]\\d{4,9}"));
  
          System.out.println("-------------------------");
  
          System.out.println("a".matches("[abc]"));  //true
          System.out.println("z".matches("[abc]"));  //false
          System.out.println("ab".matches("[abc]")); //false  因为这样[abc]只能匹配字符串一个字符所以false所以要改成[abc][abc]这个就是true
  
          System.out.println("-------------------------");
  
  
          //[^abc]  ^取反的意思
          System.out.println("a".matches("[^abc]"));  //false
          System.out.println("z".matches("[^abc]"));  //true
          System.out.println("zz".matches("[^abc]"));  //false
          System.out.println("zz".matches("[^abc][^abc]"));//true
  
  
          System.out.println("---------------------------");
          //[a-zA-Z]可以是a-z的大写和小写
          System.out.println("a".matches("[a-zA-Z]")); //true
          System.out.println("Z".matches("[a-zA-Z]")); //true
          System.out.println("aa".matches("[a-zA-Z]"));//false    //[a-zA-Z][a-zA-Z] true
          System.out.println("zz".matches("[a-zA-Z]"));//false
          System.out.println("0".matches("[a-zA-Z]"));//false    //[a-zA-Z0-9] false  //[0-9] true
  
  
          System.out.println("----------------------");
          //[a-d[m-p]] a到d，或m到p
          System.out.println("a".matches("[a-d[m-p]]")); //true
          System.out.println("d".matches("[a-d[m-p]]")); //true
          System.out.println("m".matches("[a-d[m-p]]")); //true
          System.out.println("p".matches("[a-d[m-p]]")); //true
          System.out.println("e".matches("[a-d[m-p]]")); //false   //e不在范围内所以是false
          System.out.println("0".matches("[a-d[m-p]]")); //false  //0是数字正则匹配里面没有数字
  
          System.out.println("--------------------------");
  
  
  
          //[a-z&&[def]]
          //其实就是它们的交集  def
          System.out.println("d".matches("[a-z&&[def]]")); //true
          System.out.println("a".matches("[a-z&&[def]]")); //false
          System.out.println("0".matches("[a-z&&[def]]")); //false
  
  
          //[a-z&&[^bc]]  除了bc字母都可以
          System.out.println("-------------------");
          System.out.println("a".matches("[a-z&&[^bc]]"));  //true
          System.out.println("b".matches("[a-z&&[^bc]]"));  //false
          System.out.println("z".matches("[a-z&&[^bc]]"));  //true
          System.out.println("z".matches("[a-z&[^bc]]"));  //true 因为&只能当当是符号不是&&这个才是且
  
          System.out.println("-------------------------");
  
          //[a-z&&[^m-p]]  除了m-p中的字母，其它字母都可以
          System.out.println("a".matches("[a-z&&[^m-p]]")); //true
          System.out.println("m".matches("[a-z&&[^m-p]]")); //false
          System.out.println("0".matches("[a-z&&[^m-p]]")); //false
  
    }
  }
  
  ```
  

#### jDK7前时间类

![image-20220924144225531](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220924144225531.png)

- Date  时间

  ![image-20220924150106666](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220924150106666.png)

- SimpleDateFormat 格式化时间

  - 作用
    - 格式化：把时间变成自己的格式
    - 解析：把字符串表示的时间变成Date

  ```
  package Day.Api.date;
  
  import java.text.ParseException;
  import java.text.SimpleDateFormat;
  import java.util.Date;
  
  public class DateTest {
      public static void main(String[] args) throws ParseException {
      
          //时间原点
          Date date1 = new Date(0L);
          System.out.println(date1); //Thu Jan 01 08:00:00 CST 1970
      
          Date date = new Date();
          System.out.println(date);
          //格式化时间YYYY年MM月dd日 HH:mm:ss E
          SimpleDateFormat s = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss E");
          String format = s.format(date);
          System.out.println(format);  //2022年09月24日 15:23:32 星期六
  
  
          //解析时间
          String d = "2022-09-24 15-26-20";
          SimpleDateFormat sp = new SimpleDateFormat("yyyy-MM-dd HH-mm-ss");
          Date parse = sp.parse(d);
          System.out.println(parse); //Sat Sep 24 15:26:20 CST 2022
  
  
      }
  }
  
  ```

- Calendar 日历

  ```
  package Day.Api.date;
  
  import java.text.ParseException;
  import java.text.SimpleDateFormat;
  import java.util.Calendar;
  import java.util.Date;
  
  public class DateTest {
      public static void main(String[] args) throws ParseException {
  
  
  
         //Calendar 是一个抽象类，不能直接new
  
          Calendar c = Calendar.getInstance();
  
          int year = c.get(Calendar.YEAR);
          int moth = c.get(Calendar.MONTH) + 1;
          int dt = c.get(Calendar.DATE);
          int week = c.get(Calendar.DAY_OF_WEEK);  // 1(星期日) 2(星期一) 3(星期二) 4(星期三) 5(星期四) 6(星期五) 7(星期六)
          System.out.println(year+"年"+moth+"月"+dt+"日"+" "+week(week)); //2022年9月24日
  
          //修改年为2023年
          c.set(Calendar.YEAR,2023);
          System.out.println(c.get(Calendar.YEAR));
          //如果想修改月份为12月，那么修改值要填11，因为Calendar的月份是少1的
          c.set(Calendar.MONTH,11);
          System.out.println(c.get(Calendar.MONTH));
      }
  
      //定义一个方法传入外国人对星期几的数字转换成中文
      public static String week(int week){
          String[] wek = {"","星期日","星期一","星期二","星期三","星期四","星期五","星期六"};
          return wek[week];
      }
  }
  
  ```

  

#### jdk8时间类

- 为什么要学jdk8新增时间相关类
  - 代码层面
    - jdk：代码麻烦 
    - jdk8：简单
      - 判断的方法
      - 计算时间间隔的方法
  - 安全层面
    - jdk：多线程环境下会导致数据安全的问题
    - jdk8：时间日期对象都是不可变的，解决了这个问题

![image-20220924165212609](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220924165212609.png)

- 时区，时间戳，带时区的时间，格式化和解析时间

  ```
  package Day.Api.date;
  
  import java.time.Instant;
  import java.time.ZoneId;
  import java.time.ZonedDateTime;
  import java.time.format.DateTimeFormatter;
  import java.util.Set;
  
  /**
   * Created with IntelliJ IDEA.
   * creator: 蔡芳灿
   * Date: 2022/9/24
   * Time: 16:37
   * 需求：
   */
  public class DateTest01 {
      public static void main(String[] args) {
  
  
          //ZoneId
          //获取java中所有支持时区
          Set<String> availableZoneIds = ZoneId.getAvailableZoneIds();
          System.out.println(availableZoneIds);
  
          //获取电脑时区
          ZoneId zoneId = ZoneId.systemDefault();
          System.out.println(zoneId); //Asia/Shanghai
          //设置指定的时区
          ZoneId of = ZoneId.of("Asia/Aden");
          System.out.println(of);
  
          System.out.println("---------Instant--------------");
  
          //获取的世界标准时间对象，如果想获取当前时间小时需要加8个小时
          Instant now = Instant.now();
          System.out.println(now);
  
          /**
           * 根据（秒/毫秒/纳秒）获取Instant对象
           */
          //根据纳秒获取
          Instant instant1 = Instant.ofEpochMilli(0L);
          System.out.println(instant1);//1970-01-01T00:00:00Z
  
          //根据秒
          Instant instant2 = Instant.ofEpochSecond(1);
          System.out.println(instant2);//1970-01-01T00:00:01Z 根据时间原点加一秒
  
          //第一个参数根据秒 ，第二个参数根据纳秒
          Instant instant3 = Instant.ofEpochSecond(1L, 1000000000L);
          System.out.println(instant3);//1970-01-01T00:00:02Z
  
  
          //指定地区的时间点
          ZonedDateTime zonedDateTime = now.atZone(ZoneId.of("Asia/Shanghai"));
          System.out.println(zonedDateTime);//2022-09-25T18:40:57.110030600+08:00[Asia/Shanghai]
  
          System.out.println("----------ZonedDateTime-----------");
  
          //获取当前时区时间的对象
          ZonedDateTime now1 = ZonedDateTime.now();
          System.out.println(now1);//2022-09-25T18:46:16.151643500+08:00[Asia/Shanghai]
  
  
          System.out.println("-----------------DateTimeFormatter---------------");
          DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy年MM月dd日 HH:mm:ss");
          String format = dateTimeFormatter.format(now1);
          System.out.println(format);
  
      }
  
  }
  
  ```

#### 包装类

- 什么是包装类
  - 基本数据类型对应的对象
- JDK5新增的特性
  - 自动装箱
  - 自动拆箱
- 各个基本类型的包装类

![image-20220929215914294](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20220929215914294.png)

​						

```
package Day.packaging;

/**
 * Created with IntelliJ IDEA.
 * creator: 蔡芳灿
 * Date: 2022/9/29
 * Time: 21:56
 * 需求：
 */
public class TestInteger {

    public static void main(String[] args) {

        //包装类，数字引用数字类型 Jdk5写法
        //利用构造方法来创建对象
        System.out.println("----------构造法创建对象---------------");
        Integer a = new Integer(10);
        Integer a1 = new Integer("10");
        System.out.println(a);
        System.out.println(a1);

        System.out.println("--------------静态方法创建对象------------------");

        //利用静态方法创建对象
        Integer in = Integer.valueOf(10);
        Integer integer = Integer.valueOf("123");
        Integer integer1 = Integer.valueOf("123", 8);
        System.out.println(in);
        System.out.println(integer);
        System.out.println("输出8进制的数:"+integer1);

        Integer c=10;
        System.out.println(c);


        //两个创建的对象区别
        //这个判断的是数字如果数字不在-128~127那么源码中会new出来的所以超过127就是判断地址值
        Integer i5 = Integer.valueOf(127);
        Integer i6 = Integer.valueOf(127);
        System.out.println(i5==i6);  //true


        Integer i7 = Integer.valueOf(128);
        Integer i8 = Integer.valueOf(128);
        System.out.println(i7==i8);  //false


        //底下这种判断的是地址值所以是false
        Integer i1 = new Integer(127);
        Integer i2 = new Integer(127);
        System.out.println(i1==i2);//false


        Integer i3 = new Integer(128);
        Integer i4 = new Integer(128);
        System.out.println(i3==i4);//false

    }

}

```

#### 常见算法

- 查找算法

  - 基本查找    

    - 基本查找的实现

      ```
      package find;
      
      /**
       * Created with IntelliJ IDEA.
       * creator: 蔡芳灿
       * Date: 2022/9/30
       * Time: 12:52
       * 需求：查找算法
       */
      public class BasicSearch {
          public static void main(String[] args) {
      
              int[] arr = {20,30,40,60,70,90,100,120,150};
      
              //基本查找
              boolean b = basicSearch(arr, 20);
              System.out.println(b);
          }
      
      
      
          //基本查找
          public static boolean basicSearch(int Array[],int number){
              for (int i = 0; i < Array.length; i++) {
                  if (Array[i]==number){
                      return true;
                  }
              }
              return false;
          }
      
      }
      
      ```

      

  - 二分查找/折半查找

    - 二分查找前提条件是数组的数据是顺序的

    - 提高查找效率

    - 二分查找过程

      -  min和max表示当前要查找的范围
      - 中间是在min和max中间的
      - 如果要查找的元素在mid的左边，缩小范围时，min不变， max等于mid减1
      - 如果要查找的元素在mid的右边，缩小范围时，max不变，min等于mid加1

    - 二分查找的代码实现

      - ```
        package find;
        
        /**
         * Created with IntelliJ IDEA.
         * creator: 蔡芳灿
         * Date: 2022/9/30
         * Time: 12:52
         * 需求：查找算法
         */
        public class BasicSearch {
            public static void main(String[] args) {
        
                int[] arr = {20,30,40,60,70,90,100,120,150};
        
        
                int i = ErBasicSearch(arr, 30);
                System.out.println(i);
            }
        
            //二分查找
        
            /**
             *
             * @param Array
             * @param number
             * @return
             * 1, min和max表示当前要查找的范围
             * 2，中间是在min和max中间的
             * 3,如果要查找的元素在mid的左边，缩小范围时，min不变， max等于mid减1
             * 4,如果要查找的元素在mid的右边，缩小范围时，max不变，min等于mid加1
             */
            public static int ErBasicSearch(int Array[],int number){
                int max =   Array.length-1;
                int min = 0;
                while (true){
                    int mid = (max+min)/2;
                    if (min>max){
                        return -1;
                    }
                    if (Array[mid]>number){
                        max=mid-1;
        
                    }else if (Array[mid]<number){
                        min = mid+1;
                    }else  {
                        return mid;
                    }
                }
            }
        
        }
        
        ```

#### Arrays

- 常用方法

  - ```
    package Day.Api.Arrays;
    
    
    import java.util.Arrays;
    import java.util.Collection;
    import java.util.Comparator;
    
    /**
     * Created with IntelliJ IDEA.
     * creator: 蔡芳灿
     * Date: 2022/10/2
     * Time: 16:42
     * 需求：
     */
    public class MyArrayTest01 {
    
        public static void main(String[] args) {
            int[] arr = {1,2,3,4,5,6,7,8,9,10};
            System.out.println("--------Arrays toString----------------");
            //返回指定数组内容的字符串表示形式
            System.out.println(Arrays.toString(arr));  //[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    
    
            //使用二分查找查找元素
            //第一:二分查找的数组中的元素是有序的，而且是升序的
            //第二：如果查找的数据存在返回索引
            System.out.println("--------Arrays binarySearch----------------");
            System.out.println(Arrays.binarySearch(arr, 5));//4
            System.out.println(Arrays.binarySearch(arr, 10));//9
            System.out.println(Arrays.binarySearch(arr, 20));//-11
    
    
            //复制新数组
            //第一个参数是旧数组的数据
            //第二个参数是，要从数组中的复制多少个数据到新数组，如果新数组的长度大于旧数组的长度，那么后面的数据用数组的初始值
            System.out.println("--------Arrays copyOf----------------");
            int[] ints = Arrays.copyOf(arr, 20);
            System.out.println(Arrays.toString(ints));
    
    
            //排序
            System.out.println("--------Arrays sort  升序----------------");
            Integer[] array = {20, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48};
    
    //        Arrays.sort(array);
    //        System.out.println(Arrays.toString(array));
    
    
    
            //降序排序o2-o1
            //升序排序o1-o2
            Arrays.sort(array,new Comparator<Integer>(){
    
                @Override
                public int compare(Integer o1, Integer o2) {
    
                    return o2-o1;
                }
            });
            System.out.println(Arrays.toString(array));
        }
    
    }
    
    ```

    

#### lambda  JDK8

- 注意事项
  - Lambda表达式可以用来简化匿名内部类的书写
  - Lambda表达式只能简化函数式接口的匿名内部类的写法
  - 函数式接口：
    - 有且仅有一个抽象方法的接口叫做函数式接口，接口上方可以加@FunctionalInterface注解

```
package Day.Api.Arrays;

import java.util.Arrays;

/**
 * Created with IntelliJ IDEA.
 * creator: 蔡芳灿
 * Date: 2022/10/2
 * Time: 17:22
 * 需求：
 */
public class LambdaTest {
    public static void main(String[] args) {

        Integer[] array = {20, 44, 38, 5, 47, 15, 36, 26, 27, 2, 46, 4, 19, 50, 48};
        //降序排序
        // lambda表达式 ->
//        Arrays.sort(array, (Integer o1, Integer o2) -> {
//                    return o2 - o1;
//                }
//        );
        //Integer如果数据类型相同们可以省略
//        Arrays.sort(array, (o1,  o2) -> {
//                    return o2 - o1;
//                }
//        );
        //也可以省略花括号和return
        Arrays.sort(array, (o1,  o2) ->o2 - o1);
        System.out.println(Arrays.toString(array));
    }

}

```

#### 集合体系结构

- Collection：是单列集合的祖宗接口，它的功能是全部单列集合都可以继承使用的
  - 遍历方式
    - 迭代器遍历
    - 增强for遍历
    - Lambda表达式遍历

- List

  - 添加的元素是有序的、可重复、有索引

- Set

  - 添加的元素是无序、不重复、五索引

  

#### 迭代器

- 迭代器遍历
  - 迭代器在java中类是Iterator，迭代器是集合专用的遍历方式。
- Collection集合获取迭代器
- 注意事项
  - 报错NoSuchElementException
  - 迭代器遍历完毕，指针不会复位
  - 迭代器遍历时，不能用集合的方法进行增强或者删除

```
package Day;

import java.util.ArrayList;
import java.util.Iterator;

/**
 * Created with IntelliJ IDEA.
 * creator: 蔡芳灿
 * Date: 2022/10/3
 * Time: 16:56
 * 需求：迭代器遍历
 */
public class Day186 {
    public static void main(String[] args) {

        ArrayList<String> list = new ArrayList<>();
        list.add("aaa");
        list.add("bbb");
        list.add("ccc");

        Iterator<String> it = list.iterator();

        //查看集合指针位置是否有元素，如果有数就是true，没有就是false
        while (it.hasNext()){
            //使用next方法获取第一个元素，并且移动指针到集合的第二个位置
            String str = it.next();
            System.out.println(str);
        }
    }

}

```

![image-20221003172048287](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20221003172048287.png)

#### 集合遍历方式

```
package Day;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.ListIterator;

/**
 * Created with IntelliJ IDEA.
 * creator: 蔡芳灿
 * Date: 2022/10/3
 * Time: 18:49
 * 需求：List 五种遍历
 */
public class Day188 {

    public static void main(String[] args) {
        List<String> list  = new ArrayList<>();

        list.add("aaa");
        list.add("bbb");
        list.add(1,"ccc");
        System.out.println(list);

        //迭代器遍历  如果想删除元素请用迭代器遍历
        Iterator<String> it = list.iterator();
        while (it.hasNext()){
            String str = it.next();
            if ("bbb".equals(str)){
                it.remove();
            }
            System.out.println(str);
        }
        System.out.println(list);
        //列表迭代器遍历  如果想添加元素请用列表迭代器遍历
        ListIterator<String> itList = list.listIterator();
        while (itList.hasNext()){
            String str = itList.next();
            if ("aaa".equals(str)){
                itList.add("bbb");
            }
            System.out.println(str);
        }
        System.out.println(list);

        //如果单纯遍历数据请用增强for或Lambda表达式遍历
        for (String s : list) {
            System.out.print(s+" ");
        }
        System.out.println();

        list.forEach(s -> System.out.print(s+" "));

        System.out.println();
        //如果想操作索引，使用普通for
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i)+" ");
        }
    }

}

```

#### 数据结构

- 什么是数据结构

  - 计算机存储、组织数据的方式
  - 是指数据相互之间是以什么方式排列在一起的
  - 数据结构是为了更加方便的管理和使用数据，需要结合具体的业务场景来进行选择
  - 一般情况下，精心选择数据结构可以带来跟高的运行或者存储效率

- 常见的数据结构

  - 栈

    - 栈的特点：后进先出，先进后出

      ![image-20221003191448309](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20221003191448309.png)

  - 队列

    - 特点：先进先出，后进后出

      ![image-20221003191404657](https://gcore.jsdelivr.net/gh/csh1311/blogImage@main/image-20221003191404657.png)

  - 数组

    - 特点：内存连续区域，查询快，增删慢

  - 链表

    - 特点：元素是游离的，查询慢，首尾操作极快

  - 二叉树

    - 二叉查找树遍历方式
    - 前序遍历：当前节点，左子节点，右子节点
      - 中序遍历：左子节点，中子节点，右子节点
      - 后序遍历：左子节点，右子节点，当前节点
      - 层序遍历：一层一层的去遍历
  
  - 二叉查找树平衡二叉树
  
  - 红黑树
  
    - 红黑树是一种自平衡的二叉查找树，是计算机科学中用到的一种数据结构
    - 1972年出现，当时被称为平衡二叉B树。后来，1978年被修改为如今的“红黑叔”
    - 它是一种特殊的二叉树查找树，红黑树的每一个节点上都有存储位表示节点的颜色
    - 每一个节点可以是红或者黑，红黑树不是高度平衡的，它的平衡是通过“红黑规则”进行实现的
    - 红黑树规则
      - 每一个节点或是红色的，或是黑色的
      - 根节点必须是黑色的
      - 如果一个节点没有子节点或者父节点，则该节点相应的指针属性值为Nil，这些Nil视为叶节点，每个叶节点（Nil）是黑色的
      - 如果某一个节点是红色，那么它的节点必须是黑色（不能出现两个红色节点相连的情况）
      - 对每一个节点，从节点到其所有后代叶节点的简单路劲上，均包含相同的黑色节点

#### ArrayList底层原理

- 利用空参创建的集合，在底层创建一个默认长度为0的数组
- 添加一个元素时，底层会创建一个新的长度为10的数组
- 存满时，会扩容1.5倍
- 如果一次添加多个元素，1.5倍还放不下，则新床数组的长度以实际为准

#### 泛型

- 什么是泛型
  - JDK5引入的特性，可以在编译阶段约束操作的数据类类型，并进行检查

- 泛型好处
  - 统一数据类型
  - 把运行时期的问题提前到了编译期间，避免了强制类型转换可能出现的异常，因为在编译阶段类型就能确定下来
- 泛型的细节
  - 泛型中不能写基本数据类型
  - 指定泛型的具体类型后，传递数据时，可以传入该类类型或者其子类类型
  - 如果不写泛型，类型默认是Object
- 哪里可以定义泛型
  - 泛型类：在类名后定义泛型，创建该类对象的时候，确定类型
  - 泛型方法：在修饰符后面定义泛型，调用方法的时候确定类型
  - 泛型接口：在接口名后面定义泛型，实现类确定类型，实现类延续泛型
- 泛型的继承和通配符
  - 泛型不具备继承性，但是数据具备继承性

#### set集合

- 无序：存取顺序不一致
- 不重复：可以去除重复
- 无索引：没有带索引的方法，所以不能使用普通for遍历，也不能通过索引来获取元素
- set集合实现类
  - HashSet：无序、不重复、无索引
  - LinkedHashSet：有序、不重复、无索引
  - TreeSet：可排序、不重复、五索引 
    - TreeSet自定义排序规则有几种方式
      - 方法一：javabean类实现Comparable接口，指定比较规则
      - 方法二：创建集合时，自定义Comparator比较对象，指定比较规则

#### 双列集合

- 特点
  - 双列集合一次需要存一对数据，分别为键和值
  - 键不能重复，值可以重复
  - 键和值是一一对应的，每一个键只能找到自己对应的值
    - 键+值这个整体我们称之为“键值对”或者“键值对对象”在java中叫做“Entry对象”						

- HashMap

  - 特点

    - HashMap里面的一个实现类
    - 没有额外需要学习的特有方法，直接使用Map里面的方法就可以了
    - 特点都是由键决定的：无序、不重复、无索引
    - HashMap跟HashSet底层原理一模一样的，都是哈希表结构

  - HashMap基本方法

    ```
      package Day.Api.map;
      
      import java.util.HashMap;
      import java.util.Map;
      
      /**
       * Created with IntelliJ IDEA.
       * creator: 蔡芳灿
       * Date: 2022/10/5
       * Time: 21:17
       * 需求：
       */
      public class MapTest {
          public static void main(String[] args) {
              Map<String,String> map= new HashMap<>();
              //添加元素
              //put方法的细节
              //添加/覆盖
              //在添加数据的时候，如果键不存在，那么直接把键值对对象添加到map集合当中
              //在添加数据时候，如果键存在，那么会把原有的键值对对象覆盖，会把被覆盖的值进行返回
              map.put("cai","ss");
              map.put("ss","cai");
              System.out.println(map);
      
      
              //删除
              map.remove("ss");
              System.out.println(map);
      
              //判断集合中的键是否存在
              System.out.println(map.containsKey("cai"));
              System.out.println(map.containsValue("ss"));
      
              //判断集合的长度
              System.out.println(map.size());
      
      
      
              //清空集合
              map.clear();
              System.out.println(map);
              //判读集合是否为空
              System.out.println(map.isEmpty());
          }
      
      }
      
    ```

  - HashMap遍历方式

    - ```
      package Day.Api.map;
      
      import java.util.*;
      import java.util.function.BiConsumer;
      
      /**
       * Created with IntelliJ IDEA.
       * creator: 蔡芳灿
       * Date: 2022/10/5
       * Time: 21:34
       * 需求：
       */
      public class MapTestFor {
          public static void main(String[] args) {
      
              Map<String,String> map = new HashMap<>();
              map.put("xiao","di");
              map.put("dd","cc");
              map.put("ll","jj");
              map.put("aa","bb");
              System.out.println(map);
      
      
              //
      
      
              //遍历键找值
              Set<String> m = map.keySet();
              for (String key : m) {
      //            System.out.println(key);
                  String value = map.get(key);
      //            System.out.println(key+"="+value);
              }
      
      
      
              //迭代器遍历
              Iterator<String> it = m.iterator();
              while (it.hasNext()){
                  String str = it.next();
                  String s = map.get(str);
      //            System.out.println(s);
              }
      
              //Lambda表达式遍历
              m.forEach(s -> System.out.println(s));
      
      
              System.out.println("-------------键值对遍历-----------------");
      
              Set<Map.Entry<String, String>> entrySet = map.entrySet();
              for (Map.Entry<String, String> stringStringEntry : entrySet) {
                  System.out.println(stringStringEntry.getKey()+"="+stringStringEntry.getValue());
              }
      
      
              System.out.println("----------------Lambda遍历-------------");
              map.forEach(( key, value) -> System.out.println(key+"="+value));
      
          }
      
      }
      
      ```

  - HashMap总结

    - HashMap底层是哈希表结构
    - 依赖于hashCode方法和equals方法保证键的唯一
    - 如果键存储的是自定义对象，需要重写hashCode和equals方法
    - 如果值存储自定义对象，不需要重写hashCode和equals方法