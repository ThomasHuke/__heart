# go 学习

print println printf 不同

前两个使用 "这个的的的 %g", 30.4555这个是不会讲后面的数据切换到前面来的，但是只要printf是可以的。


### go语言中的断言

#### 第一种断言

```go
var a interface{}

a = 12

a.(int)




```

如果是这样的话，那么返回的就是一个value而已 如果判断不对 那么直接panic即可。😄


#### 第二种断言

```go

var a interface{}
a = 12

if value,ok := a.(int);ok {
    fmt.Println(value)
}


```

这种方式下 是有OK和value值的 上面第一种 直接返回 或者panic

#### 第三种断言

```go

var a interface{}


switch value := a.(type) {
case int:
    fmt.Println("int")
case string:
    fmt.Println("string")
default:
    fmt.Println("error")

}


```

这种方式下，括号里只需要写上type关键字 然后会返回一个value值，并且 这个 断言就可以作为 switch的 expression了
然后每个 case 就可以使用 case  int 等这种方式 记住 不是 case "int" 这种方式。因为这是  switch独有的断言。

### ...

三个点儿就是这个   ...



用途之一：为函数定义多个参数，比如：


```go
func x(args ...int){

}
```
函数x接受任意数量的int参数

用途之二：将切片拆散
```go
m := make([]int, 3)
x(m...)
```
将切片m（含有3个int型元素）拆散成单个int型作为参数调用函数x

第一种用途，是Go提供的语法糖，不过第二种用途下，还真没想出来不用...的话该怎么写，所以看起来不太像语法糖了。
