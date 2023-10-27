## Go语言的优点

自带gc(Garbage Collection)

静态编译

简单的思想，没有继承，多态，类等

丰富的库和详细的开发文档

语法层支持并发，和拥有同步并发的channel类型，使并发开发变得非常方便。

简洁的语法，提高开发效率，同时提高代码的阅读性和可维护性。

超级简单的交叉编译，仅需更改环境变量。

## Go语言的主要特征

- 自动立即回收
- 丰富的内置类型
- 函数多返回值
- 错误处理
- 匿名函数和闭包
- 类型和接口
- 并发编程
- 反射
- 语言交互性

## Go语言命名规则

Go的函数，变量，常量，自定义类型，包的命名方式都遵循以下规则：

- 首字符可以是任意的Unicode字符或者下划线

- 剩余字符可以是Unicode字符、下划线、数字
- 字符长度不限

Go只有25个关键字

```go
    break        default      func         interface    select
    case         defer        go           map          struct
    chan         else         goto         package      switch
    const        fallthrough  if           range        type
    continue     for          import       return       var
```

Go有37个保留字

```go
Constants:    true  false  iota  nil

Types:    int  int8  int16  int32  int64  
          uint  uint8  uint16  uint32  uint64  uintptr
          float32  float64  complex128  complex64
          bool  byte  rune  string  error

Functions:   make  len  cap  new  append  copy  close  delete
             complex  real  imag
             panic  recover
```
## 基本数据类型

| 类型          | 长度(字节) | 默认值 | 说明                                      |
| ------------- | ---------- | ------ | ----------------------------------------- |
| bool          | 1          | false  |                                           |
| byte          | 1          | 0      | uint8                                     |
| rune          | 4          | 0      | Unicode Code Point, int32                 |
| int, uint     | 4或8       | 0      | 32 或 64 位                               |
| int8, uint8   | 1          | 0      | -128 ~ 127, 0 ~ 255，byte是uint8 的别名   |
| int16, uint16 | 2          | 0      | -32768 ~ 32767, 0 ~ 65535                 |
| int32, uint32 | 4          | 0      | -21亿~ 21亿, 0 ~ 42亿，rune是int32 的别名 |
| int64, uint64 | 8          | 0      |                                           |
| float32       | 4          | 0.0    |                                           |
| float64       | 8          | 0.0    |                                           |
| complex64     | 8          |        |                                           |
| complex128    | 16         |        |                                           |
| uintptr       | 4或8       |        | 以存储指针的 uint32 或 uint64 整数        |
| array         |            |        | 值类型                                    |
| struct        |            |        | 值类型                                    |
| string        |            | ""     | UTF-8 字符串                              |
| slice         |            | nil    | 引用类型                                  |
| map           |            | nil    | 引用类型                                  |
| channel       |            | nil    | 引用类型                                  |
| interface     |            | nil    | 接口                                      |
| function      |            | nil    | 函数                                      |

### 数组Array

```go
1. 数组：是同一种数据类型的固定长度的序列。
2. 数组定义：var a [len]int，比如：var a [5]int，数组长度必须是常量，且是类型的组成部分。一旦定义，长度不能变。
3. 长度是数组类型的一部分，因此，var a[5] int和var a [10]int是不同的类型。
4. 数组可以通过下标进行访问，下标是从0开始，最后一个元素下标是：len-1
for i := 0; i < len(a); i++ {
}
for index, v := range a {
}
5. 访问越界，如果下标在数组合法范围之外，则触发访问越界，会panic
6. 数组是值类型，赋值和传参会复制整个数组，而不是指针。因此改变副本的值，不会改变本身的值。
7.支持 "=="、"!=" 操作符，因为内存总是被初始化过的。
8.指针数组 [n]*T，数组指针 *[n]T。
9.内置函数len和cap都返回数组长度 len(a) cap(a)
```

#### 一维数组创建以及初始化

```go
// 数组未初始化的值为该类型的默认值
var arr1 [5]int = [5]int{1, 2, 3, 4, 5}
var arr2 = [5]int{1, 2, 3, 4, 5}
var arr3 = [...]int{1, 2, 3} // 通过初始化确定数组长度
var str = [...]string{"name", "age", "hobby"}
arr1 := [...]int{1, 2, 3}
c := [5]int{2: 100, 4: 200} // 使用索引号初始化元素
```

#### 二维数组创建以及初始化

```go
var arr0 [5][5]int
var arr1 [2][3]int = [...][3]int{{1, 2, 3}, {7, 8, 9}}
a := [2][3]int{{1, 2, 3}, {4, 5, 6}}
```

### 切片Slice

需要说明，切片并不是数组或数组指针。它通过内部指针和相关属性引用数组片段，以实现边长方案

```go
1. 切片：切片是数组的一个引用，因此切片是引用类型。但自身是结构体，值拷贝传递。
2. 切片的长度可以改变，因此，切片是一个可变的数组。
3. 切片遍历方式和数组一样，可以用len()求长度。表示可用元素数量，读写操作不能超过该限制。 
4. cap可以求出slice最大扩张容量，不能超出数组限制。0 <= len(slice) <= len(array)，其中array是slice引用的数组。
5. 切片的定义：var 变量名 []类型，比如 var str []string  var arr []int。
6. 如果 slice == nil，那么 len、cap 结果都等于 0。
```

## Go基本语法

### 变量定义

```go
package main

func main() {
	// 变量类型 变量名 数据类型
    var a int // 默认为0
	var b float64 // 默认为0
	var c bool // 默认为false
	var str string // 默认空串
    var arr [3]int // 10个大小的整型数组，其余类似
    var arr = [3]int{1, 2, 3} // 直接初始化
	// 自动推到数据类型
	a := 2
	b := 2.2
	c := false
}
```

### 标准输入输出

```go
package main
import "fmt"

// 需要包含fmt包
func main() {
    var a int
	fmt.Scan(&a)
    fmt.Scanf("%d", &a) // 与c中的scanf相似
	fmt.Print(a) // 不回车
    fmt.Println(a) // 自动回车
    fmt.Printf("a value is: %d\n", a) // 格式化输出
}
```

### 流程控制语句

```go
// if 语句
if a == 2 {
	fmt.Printf("a == 2")
} else {
	fmt.Printf("a != 2")
}

// for语句
for i:= 0; i < 100; i ++ {
    fmt.Println(i)
}

// go语言中采用for语言来代替while语句
for a > 0 {
	fmt.Println(a)
	a--
}

// break与continue与C++类似
```

## 指针

## Map

map是一种无序的基于key-value的数据结构，Go语言中的map是引用类型，必须初始化才能使用

### 结构体

Go语言中没有“类”的概念，也不支持“类”的继承等面向对象的概念。Go语言中通过结构体的内嵌再配合接口比面向对象具有更高的扩展性和灵活性。

## 函数

Golang函数特点：

- 无需声明原型
- 支持不定变参
- 支持多返回值
- 支持命名返回参数
- 支持匿名函数和闭包
- 函数也是一种类型，一个函数可以赋值给变量

- 不支持嵌套，一个包不能有两个名字一样的函数
- 不支持重载
- 不支持默认参数

### 函数声明

```go
func 函数名(参数) (返回值类型，没有则没有此处) {
	函数体	
}

// 计算a + b的函数， 返回计算结果
func add(a, b int) int {
    return a + b
}
```

### 函数返回值

Go语言可以函数可以同时返回多个值

"_"标识符可用来忽略函数的返回值

### 匿名函数

匿名函数是指不需要定义函数名的一种函数实现方式。

在Go里面，函数可以像普通变量一样被传递或使用，Go语言支持随时在代码里定义匿名函数。

匿名函数由一个不带函数名的函数声明和函数体组成。匿名函数的优越性在于可以直接使用函数内的变量，不比声明

```go
package main

import (
	"fmt"
    "math"
)

func main() {
    getSqrt := func
}
```

### 闭包

闭包是由函数及其相关的引用环境组合而成的实体。

```go
func a() func() {
	i := 0

	b := func() {
		i++
		fmt.Println(i)
	}
	return b
}

func main() {
	c := a() // c指向a函数内部的b函数
	c()
	c()
	c()
	c() // a不会输出i的值
}

// 输出结果
1
2
3
```

函数b嵌套在函数a内部 函数a返回函数b 这样在执行完var c=a()后，变量c实际上是指向了函数b()，再执行函数c()后就会显示i的值，第一次为1，第二次为2，第三次为3，以此类推。 其实，这段代码就创建了一个闭包。因为函数a()外的变量c引用了函数a()内的函数b()，就是说：

当函数a()的内部函数b()被函数a()外的一个变量引用的时候，就创建了一个闭包。 在上面的例子中，由于闭包的存在使得函数a()返回后，a中的i始终存在，这样每次执行c()，i都是自加1后的值。 从上面可以看出闭包的作用就是在a()执行完并返回后，闭包使得垃圾回收机制GC不会收回a()所占用的资源，因为a()的内部函数b()的执行需要依赖a()中的变量i。

在给定函数被多次调用的过程中，这些私有变量能够保持其持久性。变量的作用域仅限于包含它们的函数，因此无法从其它程序代码部分进行访问。不过，变量的生存期是可以很长，在一次函数调用期间所创建所生成的值在下次函数调用时仍然存在。正因为这一特点，闭包可以用来完成信息隐藏，并进而应用于需要状态表达的某些编程范型中。 下面来想象另一种情况，如果a()返回的不是函数b()，情况就完全不同了。因为a()执行完后，b()没有被返回给a()的外界，只是被a()所引用，而此时a()也只会被b()引 用，因此函数a()和b()互相引用但又不被外界打扰（被外界引用），函数a和b就会被GC回收。所以直接调用a();是页面并没有信息输出。

### 延迟调用（defer）

defer是先进后出，后面的语句会依赖前面的资源，因此如果前面的资源先释放了，后面的语句就没法执行了

```go
package main

import "fmt"

func main() {
	var whatever [5]struct{}

	for i := range whatever {
		defer fmt.Println(i)
	}
}
```

#### defer特性

```go
1. 关键字 defer 用于注册延迟调用。
2. 这些调用直到 return 前才被执。因此，可以用来做资源清理。
3. 多个defer语句，按先进后出的方式执行。
4. defer语句中的变量，在defer声明时就决定了。
```

#### defer用途

```go
1. 关闭文件句柄
2. 锁资源释放
3. 数据库连接释放
```

### 异常处理

