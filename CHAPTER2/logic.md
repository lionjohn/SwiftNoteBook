# 逻辑控制

### 循环结构

* 用for-in循环的时候，我们有时并不关心循环的位置，所以可以这样使用：计算2的10次方

```
var result = 1
var base = 2
var power = 10
for _ in 1...power {
    result *= base
}
```

* 在即将到来的Swift3.0中，苹果会取消C风格的for循环，那么如何写一个可变步长的for循环呢，方法如下：

```
for i in 10.stride (through: 0, by: -0.2) {

    print("\(i)")

}
//10.stride (through: 0, by: -0.2)，表示从10到0（through）,每次递减0.2。其他改变步长的逻辑依此类推。
```

* Swift中do-while循环变成repeat-while循环，do这个关键字被错误处理的一种情况占用了，以后会介绍到。

### 选择结构

Swfit对switch语句做了一些增强功能，具体如下：

* 在Swift中，switch语句的每一个case后面，不用主动加上break，执行完这个case之后直接就会跳转出来。

```
let rating = "A"
switch rating {
case "A" :
    print("great")              //只会打印great
case "B" :
    print("just so-so")
case "C" :
    print("it's bad")
default :
    print("error")
}
```

* 我们在平时经常会用到switch去判断多个值，以前我们是这样写的：

```
//let rating = "A"
let rating = "a"
switch rating {
case "a" :       //'case' label in a 'switch' should have at least one executable statement
case "A" :
    print("great")
case "B" :
    print("just so-so")
case "C" :
    print("it's bad")
default :
    print("error")
}
```

* 这样写会报错,我们应该用如下方式来表示：

```
let rating = "a"
switch rating {
case "a","A" :
    print("great")
case "b","B" :
    print("just so-so")
case "c","C" :
    print("it's bad")
default :
    print("error")
}
```

* 在Swift中switch的变量可以不是整型，所有的基础类型都可以，如上面的例子rating是一个String类型。
* swtich语句需要穷举所有可能的取值，而在Swift中分号";"不能代表一个空语句，当需要在switch中表示空语句时，这时候可以用break或者一对括号()来表示。

```
let rating = "a"
switch rating {
case "a","A" :
    print("great")
case "b","B" :
    print("just so-so")
case "c","C" :
    print("it's bad")
default :
//    print("error")
    ;               //';'statements are not allowed
}
```

#### switch的高级用法

* Swift中switch语句不仅可以判断单值，还可以判断区间。

```
let score = 78
switch score {
case 0 :
    print("You got an egg!")
case 1..<60 :
    print("You failed.")
case 60 :
    print("Just passed")
case 61..<80 :
    print("Just so-so")
case 80..<90 :
    print("Good")
case 90..<100 :
    print("Great!")
case 100 :
    print("Perfect!")
default :
    print("Error score.")
}
```

* 用switch对元组进行判断。

```
let vector = (0,-1)
switch vector {
case (0,0) :
    print("It's origin!")
case (1,0) :
    print("It an unit vector on the positive x-axis.")
case (-1,0):
    print("It an unit vector on the negative x-axis.")
case (0,1) :
    print("It an unit vector on the positive x-axis.")
case (0,-1):
    print("It an unit vector on the negative x-axis.")
default :
    print("It's just an ordinary vector.")
}
```

* 对元组进行switch语句判断的时候，可以用下划线"_"忽略元组中某一维度的值,并且元组中也可以使用区间。

```
let point = (1,2)
switch point {
case (0,0) :
    print("It's origin!")
case (_,0) :
    print("It on the x-axis.")
case (0,_) :
    print("It on the y-axis.")
case (-2...2,-2...2) :
    print("It's near the origin.")
default:
    print("(\(point.0),\(point.1)) is just an ordinary point.")
}
```

* 在switch也可以使用元组的解包功能。

```
let point = (0,10)
switch point {
case (0,0) :
    print("It's origin!")
case (let x,0) :
    print("It on the x-axis.")
    print("The x value is \(x)")
case (0,let y) :
    print("It on the y-axis.")
    print("The x value is \(y)")
case (let x,let y) :
    print("It's just an ordinary point.")
    print("The point is (\(x),\(y))")
}
```

* switch中的新关键字：fallthrough

```
let rating = "a"
switch rating {
case "a","A" :
    print("great")
    fallthrough
case "b","B" :
    print("just so-so")
case "c","C" :
    print("it's bad")
default :
    print("error")
}
输出结果为：
great
just so-so
```

注意：fallthrough并不会判断下一个case（或default）是否符合switch的条件，而是直接跳到下一个case（或default）的逻辑中。这使得：

1. 我们不能使用fallthrough跳到一个有逻辑判断（where）语句的case中
2. 请不要使用switch和fallthrough组合复杂的判断逻辑，来代替if else。fallthrough应该用于从一般到特殊的逐层判定。

### 控制转移

#### break continue fallthrough

求x^4 - y^2 = 15*x*y在300以内的一个正整数解

* 我们以往的做法：

```
//x^4 - y^2 = 15*x*y

var gotAnswer = false
for m in 1...300 {
    for n in 1...300 {
        if m*m*m*m - n*n == 15*m*n {
            print(m,n)
            gotAnswer = true
            break
        }
    }
    if gotAnswer {
        break
    }
}
输入结果：4 4
```

* 在Swift中我们可以这么做：给最外层的循环起一个名字

```
//x^4 - y^2 = 15*x*y

findAnswer:
for m in 1...300 {
    for n in 1...300 {
        if m*m*m*m - n*n == 15*m*n {
            print(m,n)
            break findAnswer
        }
    }
}
//输出结果：4 4
```

* 这种方式不仅适用于break，continue也可以

    #### return throw

    return 会在函数部分作介绍
    throw 会在错误处理部分作介绍

### where关键字

* 往往用于判断的扩展。

```
let point = (3,-3)
switch point {
case let (x,y) where x == y :
    print("It's on the line x == y")
case let (x,y) where x == -y :
    print("It's on the line x == -y")
case let (x,y) :
    print("It's just an ordinary point")
}
```

```
let age = 19

switch age {
case 10...19 :
    print("You're a teenager")
default :
    print("You're not a teenager")

}

if case 10...19 = age {
    print("You're a teenager")
}

if case 10...19 = age where age >= 18 {
    print("You're a teenager and in a college")
}

let vector = (4,0)
if case (let x,0) = vector where x > 2 && x < 5 {
    print("It's the vector")
}
```

* 循环中也可以使用这种case-where模式

```
for i in 1...100 {
    if i % 3 == 0 {
        print(i)
    }
}

for case let i in 1...100 where i % 3 == 0 {
    print(i)
}
```

* Swift语言中的case-where模式，在特定的情况下，快速判定模式，缩短代码，增加易读性。

### guard关键字

```
func buy(money: Int , price: Int ,capacity: Int , volume: Int) {
    if money >= price {
        if  capacity >= volume {
            print("I can buy it")
        }
        else {
            print("Not enough capacity")
        }
    }
    else {
        print("Not enough money")
    }
}

func buy2(money: Int , price: Int ,capacity: Int , volume: Int) {
    guard money >= price else {
        print("Not enough money")
        return
    }

    guard capacity >= volume else {
        print("Not enough capacity")
        return
    }

    print("I can buy it")

}
```

* 其功能跟我们常用的if-else基本相同，之所以有guard这个关键字是因为苹果建议我们使用这样的代码风格，先检验边界，然后在处理核心逻辑。

