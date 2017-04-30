# 基本类型

### 常量、变量和声明

#### 常量和变量

```
//常量 let
let maxNum = 1000
//变量 var
var index = 2
```

##### 注意：

* 在Swift中，每行代码后面可以不加分好 " ; "。
* Swift语言不是弱类型的语言，每一个变量都有一个固定的类型。如下就会报错：

```
var a = 10 , b = 20 ,c = 30
a = "Hello"    
//报错：Cannot assign value of type 'string' to type 'Int'
```

* Type inference机制:当我们给一个变量赋上初值以后Swift会自动帮助我们判断来确定这个变量的类型是什么，而不需要我们标识出这个变量的类型是什么。
* 如何显示变量的具体类型：按住option键 光标移到变量处点击即可。
* 如果非要显示类型，可以在常量或变量后面加上，冒号":"来标注。

```
let str: String = "Hello"
```

* 可以声明很多个变量后在统一标注他们的类型。

```
var a, b, c: Double
```

### 常用基本类型

#### Int和UInt

* 不同位计算机下，整型所能表示数的区间是不同的，我们可以直接通过以下方式获取到当前计算机下Int类型的最大值或者最小值

```
Int.max             //9223372036854775807
Int.min             //-9223372036854775808

UInt.max            //18446744073709551615
UInt.min            //0
```

* 当赋值发生溢出时，在编译时就会提醒我们

```
var num: Int
num = 99999999999999999999999
//error: integer literal '99999999999999999999999' overflows when stored into 'Int'

var num: UInt
num = -19
//error: negative integer '-19' overflows when stored into unsigned type 'UInt'
```

* 平时开发中我们主要用到的就是Int和UInt，但Swift为了考虑到可移植性，也提供了一些其他指定位数的整型，如：Int8，Int16，Int32，Int64以及相对应的无符号类型UInt8，UInt16，UInt32，UInt64。
* 注意：除非有非常明确地需求，否则一般情况下官方文档建议我们使用Int和UInt就好。
* 当一个数很大时，我们可以通过下划线对他进行分割，这么做并且不会改变原数值，还可以让我们很好的知道这个数的位数。

```
var num: Int = 1_000_000    //等同于Int = 1000000
```

#### Float和Double

```
let imFloat: Float = 3.1415926      //3.14159
let imDouble: Double = 3.1415926    //3.1415926
```

* Swift会根据输入的小数自动判断它的浮点类型

```
let x = 3.1415926       //let x: Double
```

* 可以通过科学计数法来赋值：

```
let x = 1.25e10         //12500000000
```

* 跟整形一样，可以使用下划线对数进行分割

```
let y = 123_000.000_001 //123000.000001
```

* 类型转换问题：Swift中类型没有自动转换的功能

```
let a:Int16 = 16
let b:Int8 = 8
a + b
//error: binary operator '+' cannot be applied to operands of type 'Int16' and 'Int8'
//可以通过手动强转解决
a + Int16(b)            //24

let a:Double = 3.0
let b:Float = 0.3
a + b
//error: binary operator '+' cannot be applied to operands of type 'Double' and 'Float'
//可以通过手动强转解决
a + Double(b)            //3.3

//同理，小数与整数也不能直接运算
let a = 3
let b = 0.3
a + b
//error: binary operator '+' cannot be applied to operands of type 'Int' and 'Double'

let red = 0.3
let green = 0.5
let blue = 0.7
UIColor(red: red, green: green, blue: blue, alpha: 1)
//error: cannot convert value of type 'Double' to expected argument type 'CGFloat'
```

* 使用手动强转类型时，如果上下类型不相符，也会报错：

```
let x:UInt16 = 1500
let y:UInt8 = 20

let n = UInt8(x) + y
//Execution was interrupted, reason: EXC_BAD_INSTRUCTION (code=EXC_I386_INVOP, subcode=0x0).
```

* 从中可以看出Swift语言是强类型的语言：不仅仅表现在每一个变量都有固定的类型上，同时在运算的过程中对类型的要求也十分严格。

#### Boolean和简单的if语句

```
let imTure = true
let imFalse = false

if imTure {
    print("I'm true")
} else {
    print("I'm false")
}
```

* 注意这里的true与false首字母为小写。
* if的条件语句可以不加小括号，加上小括号也仅仅是为了强调运算的优先级。
* if语句里即使只有一行代码，但也必须加上大括号，否则会报错
* Swift会对if语句进行检测，提示冗余的判断部分，如：

```
let imTure = true
let imFalse = false

if imFalse {
    print("I'm true")
}
else if 3 + 4 == 7 {
    print ("3 + 4 == 7")
}
else {
    print ("I'm false")         //Will never be executed
}
```

* 在Swift语言中，非零数不能当做“真”来使用：

```
if 1 {
    print("1")      //error: type 'Int' does not conform to protocol 'BooleanType'
}
```

#### Tuple

元组，将多个数据放到一个数据类型中，有点类似C语言中的结构体

* 元组的赋值是在小括号中写入各个数据，数据之间用逗号分隔。元组中可以存储不同的数据类型。

```
var point = ( 5 , 2 )
var httpResponse = ( 404 , "Not Found" )
```

* 元组可以指定所包含的数据类型。

```
var point2: ( Int , Int , Int ) = ( 10 , 5 , 2 )
var httpResponse2: ( Int , String) = ( 200 , "OK" )
```

* 元组的解包

```
//方法一
var point = ( 5 , 2 )
let ( x , y ) = point
x               //5
y               //2

//方法二
var point = ( 5 , 2 )
point.0         //5
point.1         //2
//以上方式并不直观，Swift允许我们给元组内各个元素定义一个名称
//方法三
let point3 = ( x:3 , y:2 )
point3.x        //3
point3.y        //2

let point4:( x : Int , y : Int ) = ( 5 , 6 )
point4.x        //5
point4.y        //6
```

* 实例：学生是否登陆，以及登录信息

```
let loginResult = ( true , "wangxuean" )
let (isLoginSuccess , _ ) = loginResult         //使用下划线来忽略一些我们不关心的值
if isLoginSuccess {
    print("Login Success!")
}
else {
    print("Login Failed!")
}
```

* 典型的应用：一个函数可以直接返回多个数据

#### 章节补充

* 变量名不一定完全使用英文，中文甚至表情都可以。

```
let 🐅 = "老虎"
let 名字 = "wangxuean"
print ("我的名字是" + 名字)     //我的名字是wangxuean
```

* print函数

```
print ("Hello")

let x = 1 , y = 2 , z = 3
print( x , y , z )                  //1 2 3
print( x , y , z ,separator:",")    //1,2,3
//默认的separator是空格
print( x , y , z ,separator:"," , terminator : "!")    //1,2,3!
//默认的terminator是回车，自定义修改后没有回车的功能，需要则要自己标注

print ( y , "*" , z , "=" , y*z)        //不方便
//字符串插值
print ("\(y) * \(z) = \(y*z) ")         //2 * 3 = 6
```

* 在Swift中，多行注释之间还可以插入多行注释。

