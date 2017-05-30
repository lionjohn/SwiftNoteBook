# required修饰符

# 普通子类



通常情况下，一说到`required`修饰符，我们最先想到的应该就是普通类（class）的`init()`方法了。比如下面这个类：



```
class MyClass {
    var str:String
    init(str:String) {
        self.str = str
    }
}
```



当我们定义一个`MyClass`的子类（subclass）并实例化这个子类时，我们一般会如何做呢？没错，通常情况下都会是这样：



```
class MyClass {
    var str:String
    init(str:String) {
        self.str = str
    }
}

class MySubClass:MyClass {

}

var MySubClass(str:"Hello Swift")
```



大伙应该已经注意到了，在实例化`MySubClass`时，其实是继承了它父类`MyClass`的`init()`方法。那我们再来看看子类的初始化方法。

## 子类的初始化方法

如果我们在子类中添加一个`init()`方法，像这样：



```
class MyClass {
    var str:String
    init(str:String) {
        self.str = str
    }
}

class MySubClass:MyClass {
    override init(str:String) {
        super.init(str:str)
    }   
}

var MySubClass(str:"Hello Swift")
```



那么我们首先要在`init()`方法前加上`override`修饰符，表示`MySubClass`重写了其父类的`init()`方法，然后还要调用父类的`init()`方法，并将参数一并传给父类的方法。

在实际运用中，也有另外一种情况，当子类的初始化方法参数类型与父类的初始化方法参数类型不同时，我们就不必在子类的初始化方法前加`override`修饰符了，但是要把子类初始化方法的参数类型转换为符合父类初始化方法的参数类型，然后传给父类的初始化方法：



```
class MyClass {
    var str:String
    init(str:String) {
        self.str = str
    }
}

class MySubClass:MyClass
{
    init(i:Int) {
        super.init(str:String(i))
    }
}

MySubClass(i: 10)
```



## required修饰符

我们给父类的`init()`方法加上`required`修饰符后会发生什么呢，我们来看看：



```
class MyClass {
    var str:String
    required init(str:String) {
        self.str = str
    }
}

class MySubClass:MyClass
{
    init(i:Int) {
        super.init(str:String(i))
    }
     // 编译错误
}

MySubClass(i: 10)
```



我们可以看到上面的代码在编译会发生错误，因为我们没有实现父类中要去必须要实现的方法。我们应该这样写：



```
class MyClass {
    var str:String
    required init(str:String) {
        self.str = str
    }
}

class MySubClass:MyClass
{
    required init(str:String) {
        super.init(str: str)
    }

    init(i:Int) {
        super.init(str:String(i))
    }

}

MySubClass(i: 10)
```



从上面的代码示例中不难看出，如果子类需要添加异于父类的初始化方法时，必须先要实现父类中使用`required`修饰符修饰过的初始化方法，并且也要使用`required`修饰符而不是`override`。

如果子类中不需要添加任何初始化方法，我们则可以忽略父类的`required`初始化方法：



```
class MyClass {
    var str:String
    required init(str:String) {
        self.str = str
    }
}

class MySubClass:MyClass
{

}

MySubClass(str: "hello swift")
```



在这种情况下，编译器不会报错，因为如果子类没有任何初始化方法时，[Swift](http://lib.csdn.net/base/1 "undefined")会默认使用父类的初始化方法。在[Apple的文档](https://developer.apple.com/library/prerelease/mac/documentation/Swift/Conceptual/Swift_Programming_Language/Initialization.html#//apple_ref/doc/uid/TP40014097-CH18-XID_339)中也有相关描述：

> You do not have to provide an explicit implementation of a required initializer if you can satisfy the requirement with an inherited initialiser.

## required修饰符的使用规则

1. `required`修饰符只能用于修饰类初始化方法。
2. 当子类含有异于父类的初始化方法时（初始化方法参数类型和数量异于父类），子类必须要实现父类的`required`初始化方法，并且也要使用`required`修饰符而不是`override`。
3. 当子类没有初始化方法时，可以不用实现父类的`required`初始化方法。

