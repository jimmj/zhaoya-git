# `Kotlin`笔记

## 函数及变量

> 变量定义：`变量名:类型`
>
> ```kotlin
> fun sum(a:int,b:int):int{
>     return a+b
> }函数函数
> ```
>
> 函数定义关键字`fun`

- 可将表达式做为函数体，返回值自动判断

```kotlin
fun sum(a:int,b:int)=a+b
```

- 没有返回值的函数,`Uniit`可省略

```kotlin
fun printSum(a:int,b:int):Unit{
    println("sum of $a and $b is $(a+b)")
}
// 省略Unit
fun printSum(a:int,b:int){
    println("sum of $a and $b is $(a+b)")
}
```

- 定义局部变量，且只能赋值一次即只读，使用关键字`val`

```kotlin
val a: Int = 1  // 立即赋值
val b = 2   // 自动推断出 `Int` 类型
val c: Int  // 如果没有初始值类型不能省略
c = 3       // 明确赋值
```

- 可重复赋值的局部变量，使用关键字`var`

```kotlin
var x=5
```

+ 函数参数【包含默认参数】

```kotlin
fun read(b: Array<Byte>, off: Int = 0, len: Int = b.size) { /*……*/ }
```

