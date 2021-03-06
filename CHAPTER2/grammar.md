# 基本语法

在上一章节中我们已经讲到如何创建 Swift 语言的 "Hello, World!" 程序。现在我们来复习下。

如果创建的是 OS X playground 需要引入 Cocoa ：

<pre class="prettyprint prettyprinted"><span class="kwd">import</span> <span class="typ">Cocoa</span>

<span class="com">/* 我的第一个 Swift 程序 */</span>
<span class="kwd">var</span> <span class="pln">myString</span> <span class="pun">=</span> <span class="str">"Hello, World!"</span>

<span class="kwd">print</span><span class="pun">(</span><span class="pln">myString</span><span class="pun">)</span></pre>

如果我们想创建 iOS playground 则需要引入 UIKit :

<pre class="prettyprint prettyprinted"><span class="kwd">import</span> <span class="typ">UIKit</span>
<span class="kwd">var</span> <span class="pln">myString</span> <span class="pun">=</span> <span class="str">"Hello, World!"</span>
<span class="kwd">print</span><span class="pun">(</span><span class="pln">myString</span><span class="pun">)</span></pre>

执行以上程序，输出结果为：

<pre class="prettyprint prettyprinted"><span class="typ">Hello</span><span class="pun">,</span> <span class="typ">World</span><span class="pun">!</span> </pre>

以上代码即为 Swift 程序的基本结构，接下来我们来详细说明结构的组成部分。

* * *

## Swift 引入

我们可以使用 **import** 语句来引入任何的 Objective-C 框架（或 C 库）到 Swift 程序中。例如 **import cocoa** 语句导入了使用了 Cocoa 库和API，我们可以在 Swift 程序中使用他们。

Cocoa 本身由 Objective-C 语言写成，Objective-C 又是 C 语言的严格超集，所以在 Swift 应用中我们可以很简单的混入 C 语言代码，甚至是 C++ 代码。

* * *

## Swift 标记

Swift 程序由多种标记组成，标记可以是单词，标识符，常量，字符串或符号。例如以下 Swift 程序由三种标记组成：

<pre class="prettyprint prettyprinted"><span class="kwd">print</span><span class="pun">(</span><span class="str">"test!"</span><span class="pun">)</span></pre>

以上语句由 3 个符号组成：单词( **print** )、符号( **(** )、字符串( **"test"** )。

<pre class="prettyprint prettyprinted"><span class="kwd">print</span>
<span class="pun">(</span>
   <span class="str">"test!"</span>
<span class="pun">)</span></pre>

* * *

## 注释

Swift的注释与C语言极其相似，单行注释以两个反斜线开头：

<pre class="prettyprint prettyprinted"><span class="com">//这是一行注释</span></pre>

多行注释以/*开始，以*/结束:

<pre class="prettyprint prettyprinted"><span class="com">/* 这也是一条注释，
但跨越多行 */</span></pre>

与 C 语言的多行注释有所不同的是，Swift 的多行注释可以嵌套在其他多行注释内部。写法是在一个多行注释块内插入另一个多行注释。第二个注释块封闭时，后面仍然接着第一个注释块：

<pre class="prettyprint prettyprinted"><span class="com">/* 这是第一个多行注释的开头

/* 这是嵌套的第二个多行注释 */</span>

<span class="pun">这是第一个多行注释的结尾</span> <span class="pun">*/</span></pre>

多行注释的嵌套是你可以更快捷方便的注释代码块，即使代码块中已经有了注释。

* * *

## 分号

与其它语言不同的是，Swift不要求在每行语句的结尾使用分号(;)，但当你在同一行书写多条语句时，必须用分号隔开：

<pre class="prettyprint prettyprinted"><span class="kwd">import</span> <span class="typ">Cocoa</span>
<span class="com">/* 我的第一个 Swift 程序 */</span>
<span class="kwd">var</span> <span class="pln">myString</span> <span class="pun">=</span> <span class="str">"Hello, World!"</span><span class="pun">;</span> <span class="kwd">print</span><span class="pun">(</span><span class="pln">myString</span><span class="pun">)</span></pre>

* * *

## 标识符

标识符就是给变量、常量、方法、函数、枚举、结构体、类、协议等指定的名字。构成标识符的字母均有一定的规范，Swift语言中标识符的命名规则如下：

*   区分大小写，<span lang="EN-US">Myname</span>与<span lang="EN-US">myname</span>是两个不同的标识符；

*   标识符首字符可以以下划线（<span lang="EN-US">_</span>）或者字母开始，但不能是数字；

*   标识符中其他字符可以是下划线（<span lang="EN-US">_</span>）、字母或数字。

例如： userName、User_Name、_sys_val、身高等为合法的标识符，而2mail、room#和class为非法的标识符。

**注意:**Swift中的字母采用的是Unicode编码[1]。Unicode叫做统一编码制，它包含了亚洲文字编码，如中文、日文、韩文等字符，甚至是我们在聊天工具中使用的表情符号

如果一定要使用关键字作为标识符，可以在关键字前后添加重音符号（`），例如：

* * *

## 关键字

关键字是类似于标识符的保留字符序列，除非用重音符号（`）将其括起来，否则不能用作标识符。关键字是对编译器具有特殊意义的预定义保留标识符。常见的关键字有以下4种。

### 与声明有关的关键字

<table class="reference">

<tbody>

<tr>

<td>class</td>

<td>deinit</td>

<td>enum</td>

<td>extension</td>

</tr>

<tr>

<td>func</td>

<td>import</td>

<td>init</td>

<td>internal</td>

</tr>

<tr>

<td>let</td>

<td>operator</td>

<td>private</td>

<td>protocol</td>

</tr>

<tr>

<td>public</td>

<td>static</td>

<td>struct</td>

<td>subscript</td>

</tr>

<tr>

<td>typealias</td>

<td>var</td>

<td> </td>

<td> </td>

</tr>

</tbody>

</table>

### 与语句有关的关键字

<table class="reference">

<tbody>

<tr>

<td>break</td>

<td>case</td>

<td>continue</td>

<td>default</td>

</tr>

<tr>

<td>do</td>

<td>else</td>

<td>fallthrough</td>

<td>for</td>

</tr>

<tr>

<td>if</td>

<td>in</td>

<td>return</td>

<td>switch</td>

</tr>

<tr>

<td>where</td>

<td>while</td>

<td> </td>

<td> </td>

</tr>

</tbody>

</table>

### 表达式和类型关键字

<table class="reference">

<tbody>

<tr>

<td>as</td>

<td>dynamicType</td>

<td>false</td>

<td>is</td>

</tr>

<tr>

<td>nil</td>

<td>self</td>

<td>Self</td>

<td>super</td>

</tr>

<tr>

<td>true</td>

<td>_COLUMN_</td>

<td>_FILE_</td>

<td>_FUNCTION_</td>

</tr>

<tr>

<td>_LINE_</td>

<td> </td>

<td> </td>

<td> </td>

</tr>

</tbody>

</table>

### 在特定上下文中使用的关键字

<table class="reference">

<tbody>

<tr>

<td>associativity</td>

<td>convenience</td>

<td>dynamic</td>

<td>didSet</td>

</tr>

<tr>

<td>final</td>

<td>get</td>

<td>infix</td>

<td>inout</td>

</tr>

<tr>

<td>lazy</td>

<td>left</td>

<td>mutating</td>

<td>none</td>

</tr>

<tr>

<td>nonmutating</td>

<td>optional</td>

<td>override</td>

<td>postfix</td>

</tr>

<tr>

<td>precedence</td>

<td>prefix</td>

<td>Protocol</td>

<td>required</td>

</tr>

<tr>

<td>right</td>

<td>set</td>

<td>Type</td>

<td>unowned</td>

</tr>

<tr>

<td>weak</td>

<td>willSet</td>

<td> </td>

<td> </td>

</tr>

</tbody>

</table>

* * *

## Swift 空格

Swift语言并不是像C/C++，Java那样完全忽视空格，Swift对空格的使用有一定的要求，但是又不像Python对缩进的要求那么严格。

在Swift中，运算符不能直接跟在变量或常量的后面。例如下面的代码会报错：

<pre class="prettyprint prettyprinted"><span class="kwd">let</span> <span class="pln">a</span><span class="pun">=</span> <span class="lit">1</span> <span class="pun">+</span> <span class="lit">2</span></pre>

错误信息是：

<pre class="prettyprint prettyprinted"><span class="pln">error</span><span class="pun">:</span> <span class="pln">prefix</span><span class="pun">/</span><span class="pln">postfix</span> <span class="str">'='</span> <span class="kwd">is</span> <span class="pln">reserved</span></pre>

意思大概是等号直接跟在前面或后面这种用法是保留的。

下面的代码还是会报错（继续注意空格）：

<pre class="prettyprint prettyprinted"><span class="kwd">let</span> <span class="pln">a</span> <span class="pun">=</span> <span class="lit">1</span><span class="pun">+</span> <span class="lit">2</span></pre>

错误信息是：

<pre class="prettyprint prettyprinted"><span class="pln">error</span><span class="pun">:</span> <span class="pln">consecutive statements on a line must be separated</span> <span class="kwd">by</span> <span class="str">';'</span></pre>

这是因为Swift认为到1+这个语句就结束了，2就是下一个语句了。

只有这样写才不会报错：

<pre class="prettyprint prettyprinted"><span class="kwd">let</span> <span class="pln">a</span> <span class="pun">=</span> <span class="lit">1</span> <span class="pun">+</span> <span class="lit">2</span><span class="pun">;</span>  <span class="com">// 编码规范推荐使用这种写法</span>
<span class="kwd">let</span> <span class="pln">b</span> <span class="pun">=</span> <span class="lit">3</span><span class="pun">+</span><span class="lit">4</span> <span class="com">// 这样也是OK的</span></pre>

* * *

## Swift 字面量

所谓字面量，就是指像特定的数字，字符串或者是布尔值这样，能够直接了当地指出自己的类型并为变量进行赋值的值。比如在下面：

<pre class="prettyprint prettyprinted"><span class="lit">42</span>                 <span class="com">// 整型字面量</span>
<span class="lit">3.14159</span>            <span class="com">// 浮点型字面量</span>
<span class="str">"Hello, world!"</span>    <span class="com">// 字符串型字面量</span>
<span class="kwd">true</span>               <span class="com">// 布尔型字面量</span></pre>



