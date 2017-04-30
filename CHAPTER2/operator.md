# 运算表达式



### 基础运算符

#### 赋值运算符

```
var a = 3
a = 2
```

在Swift中赋值语句没有返回值，所以下面的判断语句会报错：

```
var a = 3
if a = 1 {
    print ("a = 1")
}
```

#### 数学运算符

++和--操作将在Swift3中彻底移除。为此，使用 += 1 和 -= 1。

```
var x = 10
var y = 3
var z = 0

Double(x) / Double(y)           //两个都需要强转
x / z
x % z
//编译期间就会报错：EXC_BAAD_INSTRUCTION(code=EXC_I386_INVOP,subcode=0x0)

//求余%两侧可以不是整数
let u = 2.5
let v = 1.2
u % v           //0.1
```

### 比较运算符、逻辑运算符和判断语句

* Swift提供了两个用于比较引用变量的运算符，在类的部分会具体介绍。

```
a === b
a !== b
```

### 区间运算符和for-in

* 闭区间运算符。

```
a...b           //[a,b]

for index in 1...10 {
    index
}
```

* 前闭后开区间运算符。

```
a..<b           //[a,b)
//方便遍历数组元素
for index in 0..<10 {
    index
}
```

