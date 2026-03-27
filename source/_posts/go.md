---
title: go基础
date: 2022-12-16
tags:
toc: true
---

# GO

## 环境需要

下载安装Go

https://go.dev/doc/install

编程工具

1. `VSCode`（免费
2. `GoLand`（付费）
3. Vim（免费）

运行环境

1. Go 可以在 Linux 和 Mac 上的任何终端以及 Windows 中的 PowerShell 或 cmd 上正常运行

## 重要原则

- 不要通过共享内存来通信，通过通信来共享内存

  解释：

  ​	在传统的并发编程中，常常通过多个线程共享同一个内存空间的方式来实现数据的共享和通信。这种方式虽然在某些情况下能够提高程序的效率，但是也容易出现各种并发问题，例如竞态条件、死锁、数据竞争等。这些问题不仅难以调试，而且会极大地降低程序的可靠性和性能。

  ​	Go语言采用了一种全新的并发编程模型，即CSP（Communicating Sequential Processes），它将并发通信作为程序的主要构建块，而将共享内存作为一个附属的特性。在这种模型下，不同的并发实体通过发送和接收消息来进行通信，而不是直接读写共享内存。这种方式可以避免大多数并发问题，提高程序的可靠性和可维护性。

  例子：

  ​	假设有两个并发实体 A 和 B，它们需要共享一个数据结构来进行通信。如果使用共享内存的方式，那么 A 和 B 都需要对这个数据结构进行读写操作，容易造成数据竞争和死锁等问题。而如果使用通信的方式，可以使用一个协程来维护这个数据结构，A 和 B 只需要通过通信的方式向这个协程发送消息，即可完成对数据结构的操作，从而避免了并发问题。


## 问题一

```go

#go 网络问题导致或者是访问代理服务器时出现了问题。
D:\project\go\hello>go mod tidy
go: finding module for package rsc.io/quote
example/hello imports
        rsc.io/quote: module rsc.io/quote: Get "https://proxy.golang.org/rsc.io/quote/@v/list": dial tcp 172.217.24.113:443: i/o timeout

#修改代理服务器
go env -w GOPROXY=https://goproxy.cn,direct
```

## 基础语法





### 输出打印

在go中使用打印语句，需导入fmt，该包是您安装 Go 时获得的标准库包之一

```
// 导入Go的标准库
import "fmt"
// 定义一个main函数，main运行包时默认会执行一个函数main
func main()  {
		s := "hello"
	n := 123
	p := point{1, 2}
	fmt.Println(s, n) //hello 123
	fmt.Println(p)    //{1 2}

	fmt.Printf("s=%v\n", s)  //s=hello
	fmt.Printf("n=%v\n", n)  //n=123
	fmt.Printf("p=%v\n", p)  //p={1 2}
	fmt.Printf("p=%+v\n", p) //p={x:1 y:2}
	fmt.Printf("p=%#v\n", p) //p=main.point{x:1, y:2}

	f := 3.141592653
	fmt.Println(f)  //3.141592653
	fmt.Printf("%.2f\n", f)  //3.14
}
```

运行结果

```
您好，我是初学者
您好，我是初学者不换行
```

### 变量

定义变量有两种方法：通过这种方式一般会通过value的值来自动推导出当前name是什么数据类型

1. 使用var name = value 来声明

2. 使用 name := value 来声明

   ```
   
       //可以使用var定义变量
       var a = "init"
       // 定义了两个变量，两个变量的类型是整形
       var b,c int = 1,2
       
       var d = true
   
       var e float64
   
       f:= float32(e)
   
       // 拼接字符串
       g := a+"拼接字符串"
       fmt.Println(a,b,c,d,e,f) //init 1 2 true 0 0
       fmt.Println(g) //init拼接字符串
   ```

常量的定义

1. 使用const  name = value

   ```
       const s string = "console"
       const h = 500000000
       const t = 3e20
       fmt.Println(s,h,t)  //console 500000000 3e+20
   
   
   ```

### if else

```
    // 如果
   if 7%2==0{
        fmt.Println("7 是偶数")   
    }else{// 否则
        fmt.Println("7 是奇数") //7 是奇数
    }

    if num := 9;num<0{
        fmt.Println(num,"是负数")
    }else if num <0 {
        fmt.Println(num,"只有一位数字")
    }else{
        fmt.Println(num,"有多个数字")
    }
```

### 循环

```

    //定义一个死循环
    i := 1
    for {
        fmt.Println("loop")
        // 可以使用break停止循环
        break
    }


    // 定义一个变量j=7 如果循环>=9那么就停止循环
    for j:=7; j<9;j++ {
        fmt.Println(j)  //7 8
    }
    // 定义一个for循环，循环0~5
    for n:=0 ; n<5; n++ {
        // 如果n%2==0 那么直接跳过当前循环
        if n%2 ==0 {
            continue
        }
        // 如果不是那么打印当前n的值
        fmt.Println(n)  //1  3
    }

    for i<=3 {
        fmt.Println(i)
        i = i+1
    }
```

### switch

`switch`语句默认是不允许贯穿执行的。在Java中，需要使用`break`语句来跳出`switch`块，否则会继续执行后续的`case`分支。而在Go语言中，`switch`语句也是默认不贯穿执行的，不需要使用`break`来中断，每个`case`分支会自动退出。

```
    a:=2
    switch a {
    case 1 :
        fmt.Println("1")
    case 2 : 
        fmt.Println("2")
    case 3:
        fmt.Println("3")
    case 4,5:
        fmt.Println("4,5")
    default:
        fmt.Println("其他")
    }

    t:=time.Now()
    switch {
    case t.Hour() <12:
        fmt.Println("在中午之前")
    default:
        fmt.Println("在中午之后")
    }

```



### 数组

数组类型定义指定长度和元素类型，列如你可以这样定义数组，但这样定义数组，数组的长度已经固定了

```
var a [4]int 
// 给数组定义值
a[0] = 1
// 将数组中的第一个元素赋值给i变量
i := a[0]
// 此时i的值为
i==1
```

数组不需要初始化数据，如果是整形的数组，那么默认的值是0

```
// a[2] == 0, 没有向a数组的第三个元素赋值所以会显示默认值的0
```

go的数组数据存储

1. 栈上存储

   如果数组在函数内部声明，并且数组的大小是一个常量，那么该数组会被分配在函数的栈帧上。栈上的数组在函数返回时会被自动销毁。

   ```
   func example() {
       array := [5]int{1, 2, 3, 4, 5}
   }
   ```

2. 堆上存储

   如果数组是通过使用`new`关键字进行动态分配或者作为结构体的成员，那么该数组会被分配在堆上。堆上的数组在没有被引用时会由垃圾回收器自动回收。

   ```
   func example() {
       array := new([5]int)
   }
   
   type MyStruct struct {
       array [5]int
   }
   ```

### 切片`Slices`

数组存储数据，给定了长度是不会发生改变的，有点不灵活，在Go代码中你不会经常看见数组，然而，切片无处不在。

创建一个切片

```

    /*
    *内置函数创建切片
    *第一个参数：切片的数据类型
    *第二个参数：切片的长度
    *第三个参数：切片的容量
    */

    s := make([]int,5,5)
    
    
    //第二种方式
    d := []byte{'r', 'o', 'a', 'd'}
```

容量的作用：容量（capacity）在切片中的作用是决定切片可以扩展的最大限度，以及是否需要进行切片的扩容操作。当切片的长度超过容量时，会触发扩容操作，以提供足够的空间来容纳新的元素。

```
package main

import "fmt"

func main() {
    s := make([]int, 3, 5)
    fmt.Println("长度:", len(s))     // 输出: 3
    fmt.Println("容量:", cap(s))     // 输出: 5

    s = append(s, 1, 2, 3, 4, 5)
    fmt.Println("长度:", len(s))     // 输出: 8
    fmt.Println("容量:", cap(s))     // 输出: 10

    s = append(s, 6)
    fmt.Println("长度:", len(s))     // 输出: 9
    fmt.Println("容量:", cap(s))     // 输出: 10

    s = append(s, 7)
    fmt.Println("长度:", len(s))     // 输出: 10
    fmt.Println("容量:", cap(s))     // 输出: 10

    s = append(s, 8)
    fmt.Println("长度:", len(s))     // 输出: 11
    fmt.Println("容量:", cap(s))     // 输出: 20
}
```

切片的优点

1. 动态长度：切片的长度是动态的，可以根据需要进行动态调整，你可以随意添加和删除元素，无需考虑内存和大小

2. 灵活性：你可以使用切片进行切割、连接、追加、复制等操作，方便地处理和操作数据。

3. 内存效率：切片通过引用底层数组的方式进行操作，而不需要像数组一样进行值复制。这使得切片在内存使用方面更加高效，尤其在处理大量数据时更为显著

4. 安全性：切片提供了内置的边界检查机制，保证在访问元素时不会发生越界错误。这增加了代码的安全性，避免了许多与数组相关的运行时错误。

5. 传递和引用的灵活性：切片是引用类型，可以通过传递切片的引用来共享数据。这意味着在函数间传递切片时，不会进行切片的复制，可以高效地共享和修改数据。

   ```
   package main
   
   import "fmt"
   
   func modifySlice(s []int) {
       s[0] = 100 // 修改切片的第一个元素
   }
   
   func main() {
       original := []int{1, 2, 3}
       fmt.Println("原始切片:", original)
   
       modifySlice(original) // 传递切片的引用
   
       fmt.Println("修改后的切片:", original)  // [100 2 3]
   }
   ```

6. 支持切片操作：切片支持强大的切片操作语法，例如切片表达式 `[start:end]`、切片截取、切片追加等。这些操作使得对切片进行截取、过滤、连接等常见操作变得非常方便。

   ```
       a := []int{1, 2, 3}
       fmt.Println(a[1:2])  //[2]
       fmt.Println(a[0:])    //[1 2 3]
       fmt.Println(a[:2])    //[1 2]
       fmt.Println(a[:])   //[1 2 3]
   
   ```

   切片不会复制切片的数据。它创建一个指向原始数组的新切片值,如果过你修改切片的数据，原始数据也会跟着发生改变

   ```
   	b := a[:2]
       fmt.Println(b) //[1 2]
       b[1] = 6
       fmt.Println(b)   //[1 6] 
       fmt.Println(a)   //[1 6 3]
   ```

7. 配合内置函数和标准库：切片广泛用于与内置函数和标准库进行交互。许多内置函数和标准库函数都支持接受和返回切片类型，使得处理和操作数据变得更加方便和高效。

切片增长

要增加切片的容量，必须创建一个新的、更大的切片并将原始切片的内容复制到其中。

```
    // 创建一个切片长度为5 容量为5
    s := make([]byte, 5, 5)
    // 打印切片s
    fmt.Println(s)  //[0 0 0 0 0]
    // 打印切片s的容量
    fmt.Println(s)  //5
    // 创建一个新切片，新切片的容量是原始切片的容量的+1后的两倍
    t := make([]byte, len(s), (cap(s)+1)*2) // +1 in case cap(s) == 0
    // 打印切片t的容量
    fmt.Println(cap(t)) // 12
    // 赋值原始切片s的内容到t切片上
    for i:= range s {
        t[i] = s[i]
    }
    // 然后在将切片t赋值给s这就使切片s容量增加
    s=t 
    fmt.Println(cap(5))  // 12
    
```

使用赋值原始切片s的内容到t切片上，可以使用`Go`内部的函数copy

```
func copy(dst, src []T) int
```

优化以上的代码

```
    // 创建一个切片长度为5 容量为5
    s := make([]byte, 5, 5)
    // 打印切片s
    fmt.Println(s)  //[0 0 0 0 0]
    // 打印切片s的容量
    fmt.Println(s)  //5
    // 创建一个新切片，新切片的容量是原始切片的容量的+1后的两倍
    t := make([]byte, len(s), (cap(s)+1)*2) // +1 in case cap(s) == 0
    // 打印切片t的容量
    fmt.Println(cap(t)) // 12
    // 赋值原始切片s的内容到t切片上
	copy(t, s)
    // 然后在将切片t赋值给s这就使切片s容量增加
    s=t 
    fmt.Println(cap(5))  // 12
    
```

### map

```
 // 创建一个map key的类型是string，值的类型是int
    m := make(map[string]int)
    //给map添加元素
    m["one"] = 1
    m["two"] = 2
    // 查看map中的所以元素
    fmt.Println(m) //map[one:1 two:2]
    // 查看map的长度
    fmt.Println(len(m)) //2
    // 查看map中是否有这个元素,如果存在返回该name的值，不存在返回0
    fmt.Println(m["one"])  //1
    fmt.Println(m["sds"])  //0


    //删除map里面的数据,根据key来删除
    delete(m,"one")
    fmt.Println(m)   //map[two:2]


    // 定义一个map
    m2:=map[string]int{"one":1,"two":2}
    var m3 = map[string]int{"one":1,"two":2}
    fmt.Println(m2,m3)  //map[one:1 two:2] map[one:1 two:2]

```

### range

```
   // 定义一个切片
    nums := []int{2,3,4}
    //使用range 逗号前面i是切片的索引，逗号后面的num是切片中的值
    for i,num := range nums {
        if num==2 {
            fmt.Println("index:",i,"num",num) //index: 0 num 2
        }
    }

    m := map[string]string{"a":"A","b":"B"}
     //使用range遍历map 逗号前面k是map的key，逗号后面的v是map中的值
    for k,v := range m {
        fmt.Println(k,v) //b B ; a A
    }

    for k:= range m {
        fmt.Println("key",k) //key a;key b
    }
```

### 函数

创建函数

```
// 创建一个加法函数
func add(a int,b int) int {
    return a+b;
}

func add2(a,b int) int {
    return a+b;
}

func exists(m map[string]string,k string) (v string,ok bool){
    v,ok = m[k]
    return v,ok
}
```

函数调用

```
func main() {
 	res := add(1,2)
    fmt.Println(res)

    v , ok := exists(map[string]string{"a":"A"},"a")
    fmt.Println(v,ok)  //A true
}
```

### 指针

```

func add2(n int)  {
    n+=2
}
 // 参数声明一个整数类型的指针
func add2ptr(n *int){
    *n+=2
}

```

调用函数

```
   // 定义一个变量n
    n :=5 
    //调用add2函数
    add2(n)
    fmt.Println(n) //5

    // 调用add2ptr函数时 &n表示n的内存地址
    add2ptr(&n)
    fmt.Println(n) //7
```

### 结构体

在Go语言中，结构体（Struct）是一种自定义的数据类型，用于组合不同类型的数据字段。结构体可以包含零个或多个字段，每个字段可以是不同的数据类型。通过定义结构体，可以将多个相关的数据字段组合在一起，形成一个独立的数据单元，方便对数据进行管理和操作。

创建一个user的结构体

```
type user struct{
    name string
    password string
}
```

给结构体添加内容

```
    a:= user{name:"cc",password:"123456"}
    b := user{"cc","123456"}
    c := user{name:"cc"}
    fmt.Println(a,b,c)  //{cc 123456} {cc 123456} {cc }

    var d  user
    d.name = "cc"
    d.password = "123456"

    fmt.Println(d)  //{cc 123456}
    fmt.Println(checkPassword(a,"123456"))   //true
    fmt.Println(checkPassword2(&a,"123456"))  //true
```

```
func checkPassword(u user,password string) bool {
    return u.password == password
}

func checkPassword2(u *user,password string) bool {
    return u.password == password
}
```

### 字符串操作

1. Contains:检查字符串中是否存在这个字符
2. Count：统计字符串中某个字出现的次数
3. HasPrefix：检查字符串是否以某个字开头
4. HasPrefix：检查字符串是否以某个字结尾
5. Index：检查字或字母出现的位置
6. Join:拼接数组的字符串
7. Repeat:使字符串重复多少次
8.  Replace:替换每个字符串中的某个字或字母的
9. Split：字符串切割切割，得到的是一个数组
10.  ToLower： 将字符串的字母全部是小写
11. ToUpper： 将字符串的字母全是大写
12. len():获取字符串的长度

```
	a := "hello"
	// 使用Contains函数检查a字符串中是否存在ll的单词
	fmt.Println(strings.Contains(a, "ll")) //true
	// Count统计字符串中l出现的次数
	fmt.Println(strings.Count(a, "l")) //2
	// HasPrefix检查字符串是否以he开头
	fmt.Println(strings.HasPrefix(a, "he")) //true
	//HasSuffix检查字符串是否以llo结尾
	fmt.Println(strings.HasSuffix(a, "llo")) //true
	// Index检查ll出现的位置
	fmt.Println(strings.Index(a, "ll")) //2
	//Join 拼接数组的字符串
	fmt.Println((strings.Join([]string{"he", "llo"}, "-"))) //he-llo
	// Repeat 使字符串重复多少次
	fmt.Println(strings.Repeat(a, 2)) //hellohello
	// Replace替换
	fmt.Println(strings.Replace(a, "e", "E", -1)) //hEllo
	// Split字符串切割以-切割，得到的是一个数组
	fmt.Println(strings.Split("a-b-c", "-")) //[a b c]
	// ToLower 将字符串的字母全部是小写
	fmt.Println(strings.ToLower(a)) //hello
	// ToUpper 将字符串的字母全是大写
	fmt.Println(strings.ToUpper(a)) //HELLO
	// 获取字符串的长度
	fmt.Println(len(a)) //5
	b := "您好"
	fmt.Println(len(b)) //6
```

### JSON处理

```
	type userInfo struct {
	Name  string
	Age   int `json:"age"`
	Hobby []string
	}

	
	
	
	a := userInfo{Name: "cc", Age: 18, Hobby: []string{"Glange", "TypeScript"}}
	fmt.Println(a)
	//用于将 Go 中的数据结构转换为 JSON 格式的字节切片
	buf, err := json.Marshal(a)
	if err != nil {
		panic(err)
	}
	fmt.Println(buf)         //[123 34 78 97 109 101 34 58 3 ...]
	fmt.Println(string(buf)) //{"Name":"cc","age":18,"Hobby":["Glange","TypeScript"]}
	//json.MarshalIndent 会按照一定的格式进行缩进和换行，使得生成的 JSON 字符串更易读。
	buf, err = json.MarshalIndent(a, "", "\t")
	if err != nil {
		panic(err)
	}
	fmt.Println(string(buf))

	var b userInfo
	err = json.Unmarshal(buf, &b)
	if err != nil {
		panic(err)
	}
	fmt.Printf("%#v\n", b)  //main.userInfo{Name:"cc", Age:18, Hobby:[]string{"Glange", "TypeScript"}}
```

时间处理

```
// 获取当前时间
	now := time.Now()
	fmt.Println(now) //2023-07-27 13:01:48.2834881 +0800 CST m=+0.001977901
	// 指定时间
	t := time.Date(2023, 7, 27, 1, 25, 36, 0, time.UTC)
	t2 := time.Date(2024, 7, 27, 2, 30, 36, 0, time.UTC)
	fmt.Println(t)  //2023-07-27 01:25:36 +0000 UTC
	fmt.Println(t2) //2024-07-27 02:30:36 +0000 UTC

	fmt.Println(t.Year(), t.Month(), t.Day(), t.Hour(), t.Minute()) //2023 July 27 1 25
	fmt.Println(t.Format("2023-01-02 15:04:05"))                    //27271-07-27 01:25:36
	diff := t2.Sub(t)
	fmt.Println(diff)                           //8785h5m0s
	fmt.Println(diff.Minutes(), diff.Seconds()) //527105 3.16263e+07
	t3, err := time.Parse("2006-01-02 15:04:05", "2023-07-27 01:25:36")
	if err != nil {
		panic(err)
	}
	fmt.Println(t3 == t)    //true
	fmt.Println(now.Unix()) //1690435191
```

数字解析

```
// 字符串转小数
	f, _ := strconv.ParseFloat("1.234", 64)
	fmt.Println(f) //1.234

	// 字符串转整形
	n, _ := strconv.ParseInt("111", 10, 64)
	fmt.Println(n) //111

	n2, _ := strconv.Atoi("123")
	fmt.Println(n2)

	n3, err := strconv.Atoi("AAA")
	fmt.Println(n3)  //0
	fmt.Println(err)  //strconv.Atoi: parsing "AAA": invalid syntax
```



### 模块调用

1. 创建一个文件夹 greetings

2. 进入文件夹

3. 初始化模块

   ```
   go mod init ccsh.com/greetings
   ```

   1. `go`：这是Go编程语言的命令行接口。
   2. `mod`：它是"module"的缩写，用于与Go模块进行交互。
   3. `init`：这是`go mod`的一个子命令，用于初始化一个新模块。
   4. `ccsh.com/greetings`：这是模块的路径，也可以说是模块的名称。它通常遵循反向域名表示法，但可以是任何有效的Go导入路径。

   

4. 创建一个名为`greetings.go`的文件

5. 在文件中写入一下内容

   ```
   // 包名
   package greetings
   // 导入标准库
   import "fmt"
   
   // 创建一个函数名为hello,函数需要接收一个字符串(string)类型的名称（name）
   //这个函数有返回值类型，返回值类型市字符串（string)
   func Hello(name string) string {
       // 声明一个message变量来保存您的问候语
       // := 相当于var message string 
       message := fmt.Sprintf("Hi, %v. Welcome!", name)
       return message
   }
   ```

6. 在更目录下创建一个名为hello的的文件夹

   ![image-20230712162829109](D:\project\blogImage\image-20230712162829109.png)

7. 进入文件夹初始化模块，跟上一步的内容一样

   ```
   go mod init ccsh.com/hello
   ```

   

8. 创建一个名为`hello.go`文件

   ```
   package main
   
   import (
       "fmt"
       // 导入greetings
       "ccsh.com/greetings"
   )
   
   func main() {
       // 在这里调用了greetings模块中的Hello函数并传入了一个名为ccsh
       message := greetings.Hello("ccsh")
       // 打印输出
       fmt.Println(message)
   }
   ```

   在命令行中使用，该命令的作用是将 `ccsh.com/greetings` 这个模块的导入路径替换为相对路径 `../greetings`，也就是将远程的模块替换为本地的模块。

   ```
    go mod edit -replace ccsh.com/greetings=../greetings
   ```

   在命令行中使用,当你通过运行 `go mod tidy` 命令时，Go 命令行工具会分析你的代码中导入的包，并与 `go.mod` 文件中的依赖项进行比较。如果发现依赖项有变化，它会自动更新 `go.mod` 文件中的依赖项版本要求

   ```
   go mod tidy
   ```

   最终`go.mod `中

   ```
   module ccsh.com/hello
   
   go 1.20
   
   replace ccsh.com/greetings => ../greetings
   
   require ccsh.com/greetings v0.0.0-00010101000000-000000000000
   
   ```

   运行结果

   ![image-20230712165347361](D:\project\blogImage\image-20230712165347361.png)

### 返回并处理错误

greetings模块中的Hello函数传入的是姓名，打印的是问候语，如果你传入的字符串中是空的，那么打印的问候语就没有意义了，所以在这里需要做一个异常处理

1.  greetings模块中导入errors库

   ```
   package greetings
   
   import (
       "errors"
       "fmt"
   )
   
   // 这里返回值两个一个是strin类型一个是error类型
   func Hello(name string) (string, error) {
       //如果name的值为空直接提示
       if name == "" {
           return "", errors.New("空的 name")
       }
   
       //如果name值不为空，那么直接嵌入在Sprintf并返回生成的字符串。
       message := fmt.Sprintf("Hi, %v. Welcome!", name)
       return message, nil
   }
   ```

   

2. 在hello模块中

   - `SetFlags`这个函数中传入的参数可以是,你可以通过按位或（`|`）操作将这些标志位选项组合起来。例如，要同时显示日期和时
     - `log.Ldate`：显示日期（2009/01/23）。
     - `log.Ltime`：显示时间（`01:23:45`）。
     - `log.Lmicroseconds`：显示微秒级时间（`01:23:45.678`）。
     - `log.Llongfile`：显示完整文件路径和行号。
     - `log.Lshortfile`：显示文件名和行号。
     - `log.LUTC`：使用` UTC `时间。

   ```
   package main
   
   import (
       "fmt"
       "log"
       "ccsh.com/greetings"
   )
   
   func main() {
       // 这行代码设置了日志记录前缀  比如：greetings: 
       log.SetPrefix("greetings: ")
       // 用于设置日志记录的标志位选项  SetFlags(0)为禁用
       log.SetFlags(log.Ldate | log.Ltime)
       //message 和 err 是使用多重赋值的方式声明的变量
       message , err := greetings.Hello("")
       // fmt.Println(err)
       if err != nil {
           //使用日志包的 Fatal 函数打印错误并停止程序
           log.Fatal(err)
       }
       fmt.Println(message)
   }
   ```

3. 运行结果

   ```
   D:\project\go\hello>go run .
   greetings: 2023/07/12 23:18:36 空的 name
   exit status 1
   ```

## Goroutine（协程）

Goroutine 是 Go 语言中的并发执行单元。它是 Go 语言并发编程的核心概念，用于实现轻量级的并发处理。

在传统的多线程编程中，操作系统线程是执行计算的基本单位，每个线程都有自己的堆栈空间和寄存器等，创建和销毁线程的开销较大。而 Goroutine 则是 Go 语言中更高级的抽象，可以看作是比线程更轻量级的执行单元。

Goroutine 的特点和优势：

1. 轻量级：相比于传统的操作系统线程，Goroutine 使用的资源更少。在 64 位系统上，一个 Goroutine 的栈空间通常只有几千字节，而线程的栈空间通常是以兆字节计算的。这使得 Goroutine 可以高效地创建和销毁。
2. 并发：Goroutine 允许在同一个程序中同时执行多个任务，即并发。由于它们在运行时被调度，因此可以在多核 CPU 上并行执行，提高程序的性能。
3. 通信：在 Goroutine 之间通过通道（Channel）进行通信。通道是一种安全的、阻塞式的数据传输机制，用于在不同的 Goroutine 之间传递数据，实现数据共享和同步。
4. 容易使用：Go 语言的语法和标准库对并发编程提供了良好的支持，使得使用 Goroutine 和通道相对简单和容易。

```
func hello(i int) {
	println("hello goroutine:" + fmt.Sprint(i))
}
func HelloGoRoutine() {
	// 开启监听协程计数器
	var w sync.WaitGroup
	// 5个协程在使用
	w.Add(5)
	for i := 0; i < 5; i++ {
		// 前面加go 是创建了协程（Goroutine），每个 Goroutine 都是独立并发执行的，它们之间不会相互等待，
		// 主程序也不会等待Goroutine执行完成，有时候主程序结束结束了Goroutine都没有运行完。
		go func(j int) {
			// 协程结束，计数器-1
			defer w.Done()
			hello(j)
		}(i)
	}
	// 开启阻塞状态，直到协程结束
	w.Wait()
	// 设置等待1秒。等待所有Goroutine执行完成
	// time.Sleep(time.Second)
}

```

## Channel（通道）

Channel（通道）是一种用于在 Goroutine 之间进行通信和同步的机制。它是在多个 Goroutine 之间传递数据的管道。通过通道，不同的 Goroutine 可以安全地发送和接收数据，以实现协调和数据共享。

Channel主要特点

1. 安全性：通道提供了一种安全的数据传输机制，保证不同的Goroutine之间的数据传递是同步和有序的
2. 阻塞式操作：当相同到发送数据或从通道解释数据是，如果没有对应的解释方或发送方，通道会自动阻塞当前Goroutine。知道有对应的接收和发送操作为之，这种阻塞的特性能高有效的实现Goroutine之间的同步
3. 同时支持并发读写：通道可以同时被多个 Goroutine 读取或写入数据。它内部实现了同步机制，保证了读写操作的原子性和顺序性。

通道通信有两种：一种是有无缓冲通道，另一种是有缓冲通道

无缓冲通道：发送数据和接收数据都是阻塞的，发送数据时是阻塞的，直到有Goroutine准备接收数据，接收操作是也是阻塞的，直到有Goroutine准备发送数据

有缓冲通道：在创建是是有指定的容量的，有缓冲通道在发送数据时只有在通道已满时才会阻塞，而在接收数据时只有在通道为空时才会阻塞。当有空间时，发送操作可以立即完成，而无需等待接收方接收数据。

```
// 通道通信
func CalSquare() {
	// 创建一个无缓冲通道
	src := make(chan int)
	// 创建一个有缓冲通道
	dest := make(chan int, 3)

	// 使用无缓冲通道发送数据
	go func() {
		defer close(src)
		for i := 0; i < 10; i++ {
			src <- i
		}
	}()
	// 使用有缓冲通道接收据
	go func() {
		defer close(dest)
		for i := range src {
			dest <- i * i
		}
	}()

	for i := range dest {
		fmt.Println(i)
	}

}

```

## 并发安全（Sync）

在共享x的时候开始并发，得到的答案可能不正确，goroutine是独立运行的，因为多个 Goroutine 之间互相干扰了彼此的累加操作，导致部分操作被覆盖，结果不正确。因为多个 Goroutine 之间互相干扰了彼此的累加操作，导致部分操作被覆盖，结果不正确。

```
// 并发安全
var (
	x    int64
	lock sync.Mutex
)

func addWithLock() {
	for i := 0; i < 2000; i++ {
		// 开始互斥锁
		lock.Lock()
		x += 1
		// 释放互斥锁
		lock.Unlock()
	}
}

func addWithoutLock() {
	for i := 0; i < 2000; i++ {
		x += 1
	}
}


func main() {
	fmt.Println("Goroutine")

	 x = 0
	 for i := 0; i < 5; i++ {
	 	go addWithoutLock()
	 }
	 time.Sleep(time.Second)
	 fmt.Println("WithoutLock:", x) //WithoutLock: 6419

	 x = 0
	 for i := 0; i < 5; i++ {
	 	go addWithLock()
	 }
	 time.Sleep(time.Second)
	 fmt.Println("addWithLock:", x)  //addWithLock: 10000
}

```

