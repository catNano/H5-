## 语言基础

#### JavaScript历史

布兰登·艾奇（Brendan Eich，1961年～），1995年在网景公司，发明的JavaScript。

JavaScript诞生于1995年。它当时的目的是为了验证表单输入的验证。一开始JavaScript叫做LiveScript，但是由于当时Java这个语言特别火，所以搭上Java的顺风车，就改名为JavaScript。

同时期还有其他的网页语言，比如VBScript、JScript等等，但是后来都被JavaScript打败，所以现在的浏览器中，只运行一种脚本语言就是JavaScript。

经过许多年的发展，JavaScript从一个简单的输入验证成为一门强大的编程语言。

2003年之前，JavaScript被认为“牛皮鲜”，用来制作页面上的广告，弹窗、漂浮的广告。什么东西让人烦，什么东西就是JavaScript开发的。所以浏览器就推出了屏蔽广告功能。

2007年乔布斯发布了iPhone，这一年开始，用户就多了上网的途径，就是用移动设备上网。JavaScript在移动页面中，也是不可或缺的。并且这一年，互联网开始标准化，按照W3C规则三层分离，人们越来越重视JavaScript了。

今天，JavaScript工程师是能够和iOS、Android工程师比肩，毫不逊色的。

JavaScript是一种具有面向对象能力的、解释型的程序设计语言。更具体一点，它是基于对象和事件驱动并具有相对安全性的客户端脚本语言。

#### JavaScript的组成

##### 核心(ECMAScript)

ECMAScript是一个标准 。

因为网景的布兰登(Brendan Eich)开发了JavaScript，为了让JavaScript成为全球标准，几个公司联合ECMA（European Computer Manufacturers Association）组织定制了JavaScript语言的标准，被称为ECMAScript标准。

##### 文档对象模型(DOM)

Document Object Model。文档对象模型，后边我们会有专门的课程来讲解DOM操作

##### 浏览器对象模型(BOM)

Browser Object Model。浏览器对象模型，后边我们也会专门来讲bom操作

#### JavaScript引入及方法

```
// 对于HTML来说，从上向下同步解释性文档
// 上面的代码无法调用下面的标签或者script，下面的代码可以调用上面的标签或者script
<!-- 载入外部js，可以在head和body部分 -->
<!-- ./ 是指当前文件所在文件夹 ../上一级目录 -->
<!-- async defer 后面讲解 -->
<!-- <script src="./a.js" async defer></script> -->
<!-- 如果加载的js中，变量或者函数相同时，就会覆盖，我们叫做变量污染 -->
```

##### 内部书写

在html文件中直接进行代码的书写

  1. 位于 head 部分的脚本：

     全部的javascript代码都被下载、解析和执行完成后，才能开始呈现页面的内容（浏览器在遇到body标签才开始呈现内容）。

2. 位于 body 部分的脚本：

   为了避免上述问题，现代web应用程序一般把javascript引用放在body中，放在页面内容后面。

##### 外部引入（推荐）

​		所有的<script>元素都放在页面的<head>元素中。添加目录的时候一定要加"./"，尽量不使用"../"，禁止使用绝对路径，也可以使用网络地址。

```
<script src="./b.js"></script>
<!-- ES6的代码引入和写法，后面再描述 -->
```

优点：

1. 可维护性
2. 可缓存
3. 适应未来：通过使用外部文件包含JavaScript代码，无需使用XHTML或注释hack

注：如果加载的js中，变量或者函数相同的时候，就会覆盖，这种情况叫做变量污染

##### 直接写在标签内

```
<p onclick="alert('你好');">点击我</p>
<button onclick="console.log('aaaaa');" id='bn'>按钮</button>
<a href="javascript:console.log('aaaaa')">超链接</a>
<!-- 不跳转 -->
<a href="javascript:void(0)">超链接</a>
```

##### ES6的代码引入和写法

1. 从上向下解释性文档，上面的代码无法调用下面的标签和脚本
2. 浏览器的自动修正，script脚本放在HTML标签外面的时候，浏览器会将script标签放在body的最下面，**可利用**，但是不建议，因为会消耗浏览器的性能

#### 注释

作用：为了程序的可读性，以及便于日后代码修改和维护时，更快理解代码，你可以在 Javascript 程序里为代码写注释(comments)。注释可以让不用的代码不执行，注释可以用来解释代码的作用。

##### 	单行注释

```
// 注释内容 不可换行

ctrl+/
```

##### 	块级/多行注释

1. 块状注释可以用来注释一行中的部分内容
2. 块状注释可以用来注释掉一个函数和大量代码块
3. 块状注释对于函数的注释说明在函数部分讲解

```
/* 注释内容

可以换行 */

ctrl+shift+/

```

#### 调试

​	浏览器调试

```
ctrl+shift+i或者
F12
```

- preformance，录制操作占用内存
- memory，记录操作快照，展示内存具体使用信息

#### JS代码规则

- 分号结尾，英文半角
- 大小写严格
  - 一般首字母都是小写，除了类
  - 一般都是驼峰命名规则，即除了第一个以外，每个单词的首字母大写，其他字母小写，setWorkDay——驼峰式

#### 常用方法

###### alert()

```
alert('弹出内容');  警告消息框 //方法一般包括 方法名(参数...) 都必须是英文半角
原型为window.alert();这里是将window省略了
alert(message?:any):void
提示：message 参数名称
		? 	可以不写值
	   :any  这个参数的类型可以是任意的
	   :void 不返回任何值
alert("你好");//将字符串以弹窗弹出，并且暂停到当前行
```

###### confirm()

```
confirm()    弹出确认消息框
confirm(message?: string): boolean
var a=confirm("是否继续？");
```

###### console.log()

```
console.log()	控制台输出内容
(method) Console.log(...data: any[]): void

console.dir("aaa");
console.error("错误");
console.info("信息")
```

###### prompt()

```
prompt()    弹出输入框，提示消息框----就是专门用来给用户提供输入窗口的
prompt(message?: string, _default?: string): string
提示：_default?: string 默认值为字符串类型
```

###### document.write()

```
document.write(); //HTML文档中写入字符
Document.write(...text: string[]): void //...表示多个
document.write("<a href='#'>超链接</a>");
```

###### 注：

- js 是点语法，表示某个对象的方法和属性


- 对象有两种模式，一种是属性，属性使用=赋值，

  ​								一种是方法，方法需要()执行

- write仅属于document的方法，可以给整个文档中增加内容
  innerHTML是所有body内（含body）标签的属性，可以给这些标签内局部增加内容和标签（替换原来内容）

```
document.body.innerHTML="你好";//赋值，对象的属性需要赋值
```

```
document.body.innerHTML="<div></div>";
```

```
<div id="div0">asds</div>
<script>
	var div0=document.getElementById("div0");
    div0.style.color="red";
    div0.innerHTML="<div>sadasd</div>";
    div0.onclick=function(){
    	div0.innerHTML="点击了";
    }
</script>
```

#### 语句块

​	语句块 (blocks) 是由一些相互有关联的语句构成的语句集合。

通常来说，用 {} 括起来的一组 Javascript 语句称为语句块 (blocks)。

在语句块里面的每句语句以分号 (;) 表示结束 ，但是语句块本身不用分号。

语句块 (blocks) 通常用于函数和条件语句中

#### 变量

- ES5 IE8时代支持的js标准，2015年正式使用ES6，又称为ES2015

- JavaScript的变量是松散类型的，所谓的松散类型就是可以用来保存任何类型的数据

- 不推荐创建全局变量，污染全局命名空间

- 定义未初始化的值：undefined

- 一条语句定义多个变量，逗号分隔

- =赋值也是有返回值的，返回等号右边的值

- 连等赋值，`a=b=3`，先赋值给a，再赋值给b，运行过程是先将（b=3）的返回值赋值给a，再将3赋值给b，任何赋值都是有返回值的

- ES5中不允许直接使用变量的赋值，必须前面加一个var声明变量的赋值

- 如果函数内不使用var声明，这个变量就一定从属于window，而在函数以外的地方使用var声明，也是设置了window的属性，也从属于window

- 变量的命名规则：

  ​			1、驼峰式命名

  ​			2、临时变量必须使用下划线起头后面接驼峰式命名，有时候也会在函数的参数中使用临时变量

  ​			3、全局的变量名不能与window下的属性和方法同名，不报错，但是会覆盖本来的函数

- window下的变量status固定为字符串，使用代码提示检测变量名是否是关键字

- const常量，常量名称必须大写，并且使用下划线区分单词，使用常量的目的是，不会被别人修改或者变量污染

###### ES5之前

```
window.a=3;
a=3;
a="a";
a=b=3;//连等，先赋值给=号最左边的元素，再逐级向右，实际上是先将b=3的返回值赋值给a
a=b=3;//a=(b=3);  代码遵从从左至右的执行方式
//=号左侧是变量名称，=号右侧是值
// 不需要定义，随手写，不需要类型（弱类型）
// =号赋值也是有返回值
```

###### ES5

```
var a = 3; //定义变量，不允许直接使用变量的赋值
如果不使用var声明，那就这个变量就一定是window的属性
	window.a=3;
而在函数以外的地方使用var声明也是设置了window的属性
	console.log(window.a);
```

###### ES6

```
let  变量  放在ES6的部分讲解
const  常量  变量是定义后可以变化值的，常量是一旦定义值就不能改变值了
	常量定义：
		常量定义是名称必须全部大写，并且使用_区分单词
		使用常量目的是不会被别人修改或者变量污染改变
		const EVENT_ID="changes";
```

###### 变量的命名规则

```
1、变量必须驼峰式命名法
2、临时变量必须使用_起头，后面接驼峰式命名，有时候也会再函数的参数中使用临时变量命名
	var _a = 3;
3、变量中不可以使用关键字和保留字，使用保留字命名不报错，但是不能使用
	    // var if=3;//关键字
        // var public=10;//保留字
        // var static=20;//保留字
4、全局的变量名不能与window下的属性和方法同名
        // var alert=10;
        // console.log(alert);
        // alert("aaaa");
        // var status=10;
        // console.log(status);
```

```
// console.log(var a=3);//一旦使用var是不可以返回的
// console.log(a=3); 没有使用var会被赋值的结果返回
```



##### 	JavaScript关键字

​		关键字可用于表示控制语句的开始或结束，或者用于执行特定操作等。

按照规则，关键字也是语言保留的，不能用作标识符！

```
break		do		instanceof	typeof

case		else		new		var

catch		finally		return		void

continue	  	for		switch		while

function		this		with 		default

if 			throw		delete		in

try
```

##### 	JavaScript保留字

​		保留字有可能在将来被用作关键字来使用，不能用作标识符！

```
abstract         int                   short              boolean

export           interface         static               byte

extends         long                super              char

final              native              class	    float

throws          const               goto               private

double          import            public
```



##### 	JavaScript变量

```
1 .一次声明一个变量。例句如下：

var a; 

2 . 同时声明多个变量，变量之间用逗号相隔 。例句如下：  

var a, b, c; 
var a1=3,
    b1=4,
    c1="a",
    d1=true;
var a=b=3;//尽量不要使用连等赋值

3 .声明一个变量时，同时赋予变量初始值。例句如下：

var a=2 ; 

4 . 同时声明多个变量，并且赋予这些变量初始值，变量之间用逗号相隔 。例句如下：

var a=2, b=5;
```

##### 	JavaScript常量

​		const

#### 数据类型

​		JavaScript不支持任何创建自定义类型的机制

##### 	字符类型

​		String

​		字符型   所有使用 ''  ""  ``都是字符型  string

```
// var a="a";
// var b='1';
// var c=`true`;
// var d='你好这个非常"不错"';
// console.log(a,b,c,d);
// console.log(typeof a);
// console.log(typeof(a));
```

##### 	数值型 Number

各类进制（log会打印十进制）、整数、浮点数、带符号，科学计数法

```
// var a=3;
// var b=3.1;
// var c=-5;
// var d=-5.6;
// var e=0xFF;//16进制
// var f=065;//8进制
// var g=3.1e+5;//科学计数法 3.1*10(5)5次幂
// var h=3.5e-5;//科学计数法 3.5*10(-5) -5次幂
// console.log(typeof g,g);// number 310000
```

##### 	布尔类型 Boolean

true,false    对和错，是和否，还可以认为是任何事情的两面

```
var a=true;
var b=false;
```

布尔值的应用：

```
var div0=document.getElementById("div0");
var bool=true;//这就是布尔值;
div0.onclick=function(){
    bool=!bool;
    //将bool取反，因为这个bool值的值域只有true和false
    div0.style.backgroundColor=bool ? "red" : "blue";
        } 
```

##### 	对象 Object

- key:value  关键词和值
- 对象不能出现重复的key
- key不需要加""，可以加，但不建议

```
	var d="names";
        obj={
            a:1,
            b:"ab",
            "c":true, //不建议
            [d]:"wk" // 变量作为key必须在外层增加[]
        }
        console.log(obj.a);
        console.log(obj["a"]); //意义同上
        console.log(obj.names)；//打印names:wk
        console.log(obj[d]); //调用变量作为key的属性，意义同上
```

```
var obj={};
//空对象，算是个空盒子
obj=null;
//设值为空，盒子都扔了
```

##### 	空值 Null

- typeof输出object

  ​		原因：因为null多用于对象清空，字符类型、数值类型、布尔类型、未定义数据类型均不需要使用null进行回收

- 空值是将所有引用地址标记清空，用于清理内存垃圾回收

  ```
  var obj={a:1};
   obj=null;
  ```

##### 	未定义值 Undefined

- 仅定义变量未初始化

  ```
  var a;
  ```

- 定义变量并且设置值为undefined

  ```
  var a;
  var b=undefined;
  console.log(a===b); //true，值是相同的，数据类型相同，但是形态不同
  ```

- `var a;`  用于全局定义，然后根据需要时赋值，初始是没有值的

- `var b=undefined` 用于初始值必须是undefined，或者将原有有值的变量修改为undefined

  ```
  var x=10;
  x=undefined;
  ```

##### 	typeof操作符

​		typeof操作符用来检测变量的数据类型，是个操作符，不是函数

#### 数据类型转换

​		数据类型转换分为强制转换和隐式转换两种

##### 数值转换

1、数值转字符串

​		强制转换

```
var b=String(a); //类型强制转换
	a=String(a); //将a转换为字符串覆盖原有变量a
```

​		隐式转换

```
a=a+"";利用隐式转换方式，没有强制转换，根据运算特征自动转换为字符串，隐式转换所使用的的转换方法是自动执行String(a);
```

​		toString(number)

- 实际上是Object对象的方法，万物皆对象，任何类型都可以调用这个方法

- 参数必须是2-36之间，否则报错，转换为指定的进制数

  ```
  var a = 15;
  a = a.toString(16);
  console.log(a);
  此时输出F
  ```

  应用：

  ```
  var color=0x0000FFFF;
  var div0=document.getElementById('div0');
  div0.style.color="#"+(color<<8).toString(16);toFixed(number)
  ```

- toFixed(number)  

  参数为浮点位，表示小数点后面保存的位数，15~15.00，自动四舍五入

  ```
  a = a.toFixed(2)
  ```

- toExponential()

  1、将数值格式化为科学计数法

  2、参数值的范围是0~20

  3、参数值表示科学计数法小数点后面的位数，当数值的位数超出参数指定范围的时候，进行四舍五入

- toPrecision()

  1、将数值格式化为指定的长度，参数、表示长度

  2、当对象的值超出指定位数时，将其格式化为科学计数法，不够的时候用小数点后面的0来凑

  

2、数值转换为布尔值

- 除了0以外所有的数值转换为布尔值都是true，0转换为布尔值是false

- 强制转换（只能Boolean()强制转换）

  ```
  var a = 0;
  a = Boolean(a);
  console.log(a);
  //false
  ```

3、数值转换为对象

​			数值型对象可以加减，具有数值特征，存储在堆中

```
var a = 0;
a = Object(a);
console.log(a);
输出为0
typeof a//输出为Object
```

##### 字符串

4、字符串转换为数值

- Number() 强制换行

```
var a = "a";
a = Number(a);
console.log(a);
输出NaN
//NaN，数值类型中的非数值
如果是字符串本身就是数值的，则可以正常转换
```

- parselnt()

  1、字符串转换成整数

  2、两个参数，第一个参数是需要转换的值，第二个参数表示按照几进制接收

  ```
  var a = "101";
  a = parseInt(a,2);
  //此时输出a为5
  ```

- parseFloat() 

  字符串转换成浮点数，不能转换进制

- 注意

  1、parselnt()和parseFloat() 两个函数在转换"32a"这种的时候会转换成32，省略不符合数值特征的部分，而Number会报错，隐式转换遵从Number

  2、Number的转换，"32 "(32+空格)，--->32，"32 1"---->NaN，首尾有空格会自动去除，但是中间有不可以，会被认定为字符，但是parselnt()和parseFloat() 两个函数会省略中间空格后面的内容进行数制转换

  ```
  var b="32 1";
  var a="32 "
  
  b=Number(b); //NaN
  
  b=parseInt(b); //32
  b=parseFloat(b); //32
  
  console.log(b);//隐式转换遵从Number
  ```

5、字符串转换为布尔值

- 仅空字符串（null）转换为布尔值时，是false，除此之外全部是true
- 空格不是空字符串，空格是true

```
    var str="";
    str=Boolean(str);
    console.log(str);//true
```

6、字符串转换为对象

- 字符串转换为对象 Object() 转换后为字符串对象

```
    var str="aaa";
    str=Object(str);//转换为字符串对象
    console.log(str);
```

##### 布尔值

7、布尔转换为数值

- true转换为1，false转换为0

```
var b=true;
b=Number(b);
console.log(b);
```

8、布尔转换为字符

- 转换后就是字符串true和false

9、布尔转换为对象

- 转换后就是布尔值对象

10、任何类型转换为布尔值

- false：空字符串、0，NaN、false、null、undefined
- 除了上面六种情况均为true

##### undefined、null转换为字符串和数值

- 隐式转换undefined和null转换为字符串是undefined和null
- 隐式转换undefined和null为数值是NaN和0
- parseInt转换undefined和null为数值为NaN和NaN

#### 定义变量的常用方法

- 尽量不要使用连等赋值变量定义
- 有值变量定义最好换行定义，按照类型定义，将类型分开定义，比较清楚

#### 进制

```
十进制
0，1，2，3，4，5，6，7，8，9，10……

二进制
0，1，10，11，100，101，110，111，1000……

八进制
0，1，2，3，4，5，6，7，10，11，12，13，14……
二进制转八进制，二进制数分割为三位一组计算

十六进制
0，1，2，3，4，5，6，7，8，9，a,b,c,Sd,e,f,10……
二进制转十六进制，二进制数分割为四位一组计算

R	G	B	A	：数值越大，越亮
255	255	255	255 （十进制）
FF	FF	FF	FF	（十六进制）
0xFF0000 ：红色
```

#### 运算符

##### 	算术运算符

加(+）减(-） 乘(*）除(/）取模（%）

- 数据类型不同时：

  1、“+”号两端出现字符串的话，就会变成字符串拼接，数值、布尔值、undefined、Null通过String隐式转换为字符串

  2、“+”号两端没有出现字符串，其他非数值类型就会转换为数值并相加

  ![+运算时的数据转换](./数据转换.png)

  3、所有类型遇到“-”、“*”、“/”和“%”的时候，都会隐式转换为数值进行运算

- 浮点运算存在误差
- 加法运算符结果

##### 	一元运算符

（++）累加	（--）递减

- 累加（递减）在前，先返回后运算，以+1后的结果参加运算
- 累加（递减）在后，先运算后返回，以a参加运算，+1前
- 对于累加和递减，通常都会直接使用算数运算来处理，会先将内容隐式转换为数值，然后再运算

```
var a = "3";
var b = a++;
//b输出结果为数值3
将字符串隐式转换为数值的一种方式

这种恶心吧啦的式子随便拆
b=a+++a+++a+a+++a+a
```

##### 	关系运算符

大于>、大于等于>=、小于<、小于等于<=、等于==、严格相等===、不等!=、非严格相等!==

- 关系运算符尽可能使用三个等号，判断更严谨
- 关系运算是返回布尔值的一种运算表达式
- 判断关系时，Number,Boolean,String优先隐式转换为数值，并且比较；object对象和其他类型比较时，会调用to.string()和valueof()转为字符串，如果另外一个不是字符串，再转成数值比较。

```
console.log(""==false);
console.log(0=="");
console.log(0==false);
上面全是true

console.log(0==null);//false

console.log(undefined==null);//true，特殊，都没有数值
除了undefined==null和等于其本身，undefined，null与其他类型都不相等

console.log(NaN==NaN);//false
特殊：NaN跟任何值都不相等，包括他自身，NaN==NaN-->false
```

- isNaN  将这个字符串转换为数值后判断是否是NaN非数值

  应用：

```
        var a=0;
        if(a==false){
            console.log("aa");
            // a->  0  false  "" 
        }

        if(a===false){
            console.log("aa");
            // a-->false
        }
        if(!a){
            console.log("aa");
            // a-->0 null undefined false "" NaN
        }

        if(a==null){
            // a-->undefined  null
        }
        if(a===undefined){
            //a-->undefined
        }
```

##### 	逻辑运算符

!	逻辑非、&	逻辑与、||	逻辑或

- 得到的结果不一定是布尔值

```
true && true = (第二个值)
true && false = （第二个值）
false && true = （第一个值）
false && false = （第一个值）
```

```
true || true = (第一个值)
true || false = （第一个值）
false || true = （第二个值）
false || false = （第二个值）
```

- 逻辑非可以用了做开关、多选框的反选

  开关应用：

```
var bool=false;
var bn=document.getElementById("bn");
bn.onclick=function(){
    bool=!bool;//取反运算
    bn.innerHTML=bool ? "开" : "关";
}
```

##### 	赋值运算符

- 乘法/赋值（*=）

- 除法/赋值（/=）

- 取模/赋值（%=）

- 加法/赋值（+=）

```
var a=3;
a+=7;//a=a+7;   7就是步长 step
console.log(a+=7); //17
```

```
var a=3;
a+="";
利用隐式转换完成字符串转换
```

- 减法/赋值（-=）

- 左移/赋值（<<=）

```
var a=3;
a<<=2;
console.log(a);
var a=1;
for(var i=0;i<5;i++){
     a<<=1;
     console.log(a);
 }//2.4.8.16.32
 
var a=5;
a>>=1;
console.log(a);//2
```

- 有符号右移/赋值（>>=）

- 无符号右移/赋值（>>>=）

- 赋值运算符的优先级最低


##### 	位运算符

- 位非运算符（~） 加1取负

  ```
  var str='abcdef';
  if(~str.indexof('a')){
  	//str中是否能找到字符a,如果没有找到，返回-1
  }
  ```

- 位与运算符（&）

  ```
  例如：25 & 34		6&7
   11001				110
  100010				111
  000000 -->0			110-->6
  ```

- 位或运算符（|）

  ```
  1|1=1；1|0=1；0|1=1；
  例如：1|2=3
  ```

- 位异或运算符（^） 相同位0，不同为1

  ```
  1^2=3 
   1
  10
  11-->3
  ```

- 左移位运算符（<<）

  ```
  1<<4=16
  1*2^4=16
  ```

- 右移位运算符（>>）

##### 	三目运算符

条件语句 ？ 语句1 ：语句2;

判断条件是否成立，成立执行语句1，不成立执行语句2

- 三目运算符优先级比赋值运算符高
- 当返回的是布尔值的时候，不要使用三目运算符
- 问号前面的内容会隐式转换为布尔值
- 不要将条件运算表达式复杂化，尽量不要使用赋值运算符

```
例： var a =3>2 ? 1 : 0; //1
	var a =1>2 ? 1 : (3<4 ? 0 : -1); //0
	
	var a =1;
	a= a-- ? a++ : ++a; //0
	
	var a =1;
	var b = a-=1 ? a++ : ++a;
	1、三目运算符优先级比赋值运算符高，所以先运算 1 ? a++ : ++a; 返回值1
	2、再运算 b = a-= 1 ，先将1赋值给b
	3、再运算 a-= 1，返回a的值为0，然后再将a的值赋给b，即b = a = 0
	console.log(b,a); // 0 0

```

​		应用：

```
<input type="checkbox" id="div0">
<label for="div0" id="lables">你好</label>
<script>
var div0=document.getElementById("div0");
var lables=document.getElementById("lables");
div0.onclick=function(){
    lables.style.color=div0.checked ? "red" :"green";
}
</script>
```

#### 运算符优先级

```
   . [] ()	字段访问、数组下标、函数调用以及表达式分组
​	++ -- -(负号) ~ ! delete new typeof void	一元运算符、返回数据类型、对象创建、未定义值
​	* / %	乘法、除法、取模
​	+ - +	加法、减法、字符串连接
​	<< >> >>>	移位
​	< <= > >= instanceof	小于、小于等于、大于、大于等于、instanceof
​	== != === !==	等于、不等于、严格相等、非严格相等
​	&	按位与
​	^	按位异或
​	|	按位或
​	&&	逻辑与
​	||	逻辑或
​	?:	条件
​	= oP=	赋值、运算赋值
​	,	多重求值
```

#### 表达式

```
	avascript 表达式 (expressions) 相当于 javascript 语言中的一个短语，包括变量、字面量和运算符，这个短语可以判断或者产生一个值，这个值可以是任何一种合法的 Javascript 类型 - 数字，字符串，对象等。

最简单的表达式是字符。

表达式示例：

3.9 // 数字字符

"Hello!" // 字符串字符

false // 布尔字符

null // null 值字符

Age + 3

以下是比较复杂的表达式示例： 

3 * (4 / 5) + 6

Math.PI * radius * radius+12
```

## 流程控制语句

#### 条件语句

1. 条件不管是什么表达式，都会隐式转换为布尔值
2. 常用运算符：非！（非真进入）

##### 	if

```
if (条件表达式) {
	//如果条件表达式运算后隐式转换为布尔值时true，进入该条件语句
}
```

```
例：如果输入密码123，提示正确
例： var a =1;
	if(a*=10){
		//a*=10可以先运算，缩减代码
		console.log(a); //10
	}
例：不让小方块在大方块中出去
        var x,y
        if(x<0) x=0;
        if(x+50>500) x=500-50;
        if(y<0) y=0;
        if(y+50>500) y=500-50;
```



##### 	if else

```
if(条件表达式){
	语句1
}else{
	//条件隐式转换为布尔值为false时进入
	语句2
}
语句3
```



##### 	if  else if

```
if(条件表达式1){
	语句1
}else if(条件表达式2){
	语句2
}else if(条件表达式3){
	语句3
}
……
else{
	语句4
}//仅执行其中一个结果


if(条件表达式1){
	语句1
}
if(条件表达式2){
	语句2
}
if(条件表达式3){
	语句3
}//每个条件都会判断并执行
```



##### 	if语句的嵌套

```
if(条件){
	if(条件){
	}
}
```



##### 	switch case 多分支结构语句

```
switch(n)
{
case 值1:
	//当表达式绝对等于值1时，执行对于的内容（===）
  	代码块 1
	break; //跳出，如果不写，不判断值2是否相等，直接穿越
case 值2:
	//当表达式绝对等于值2时，执行对于的内容（===）
  	代码块 2
	break;
default:
 	//默认以上条件都不满足时执行这里
}
```

- 表达式和值1必须是严格相等才会执行语句1，值也可以是运算式

- break是必须的，如果值1没有break，程序不会判断表达式是否与值2严格相等，直接执行语句2，这种现象叫做穿越

- 穿越现象会被利用减少代码量，减少重复代码

- switch经常会被用来做状态机

  ```
  var status="";
  const RUN="run";
  const WALK="walk";
  const JUMP="jump";
  cnst FIRE="fire";
  
  status = RUN;
  switch(status){
  	case RUN:
          console.log("跑步动画");
          breack;
  	case WALK:
          console.log("走路动画");
          breack;
  	case JUMP:
          console.log("跳跃动画");
          breack;
  	case FIRE:
          console.log("开火动画");
          breack;
  	default:
  }
  ```

- 特点：严格相等、判决条件清晰、可穿越

​        应用：

```
var a = 1;
switch(a){
	case '1':
	console.log('AAA');
	break;
	case 2:
	console.log('BBB');
	break;
	default:
	console.log('CCC');
}//执行结果CCC
```

```
var a = 1;
switch(a){
	case 1:
	console.log('AAA');
	case 2:
	console.log('BBB');
	break;
	default:
	console.log('CCC');
}//执行结果AAA BBB
```

```
var score = prompt("请输入你的成绩");
switch(parseInt(score/10)){
	case 9:
		console.log("优秀");
	break;
	case 8:
		console.log("良好");
	break;
	case 7:
		console.log("一般");
	break;
}
或
switch(true){
	case score>90 && score<=100:
		console.log("优秀");
	break;
	case score>80:
		console.log("良好");
	break;
	case score>70:
		console.log("一般");
	break;
	case score>60:
		console.log("及格");
	break;
	default:
		console.log("不及格");
}
```

#### 循环语句

- 禁止出现重复代码
- 要将代码尽可能进行加精简

##### 	while

while语句是一种先判断，后运行的循环语句。也就是说，必须满足条件了之后，方可运行循环体。

1、while 先判断后循环，循环体有可能一次也不执行，循环体应包含使循环结束的语句

```
语法格式：
while（判断语句）｛
	循环体；
｝
```

- 在大量运行时，while的效率高于for，推荐使用while

2、do while 先运行后判断，至少运行一次

```
do
{
   循环体;    
   循环增量;
}while(循环条件)
```

- 常使用++i
- 使用场景较少

while应用：

- 利用循环生成10个div

```
        var i = 0;
        while(i<10){
            document.write("<div>"+i+"</div>");
            i++;
        }
        或者
        var i = -1;
        while(i++<9){
            document.write("<div>"+i+"</div>");
        }
```

- 0加到100

```
        var i =0;
        var sum = 0;
        while(i++<100){
            sum +=i;
        }
        console.log(sum);
```

- 打印十行十列*

```
       var i = 0, j;
       while(i++<10){
           j=0;
           while(j++<10){
               document.write("*");
           }
           document.write("<br>");
       }
```

- 打印列表

```
        var i = 0,j;
        document.write("<ul>");
        while (i++ < 10) {
            document.write("<li>第" + i + "章<ul>");
            j = 0;
            while (j++ < 10) {
                document.write("<li>第" + j + "节</li>");
            }
            document.write("</ul></li>");
        }
        document.write("</ul>");
```

- 打印三角形

```
        var i = 0, j, n;
        var row = 10;
        var col = 10;
        while (i++<10) {
            n = 0;
            while (n++<col-i) {
                document.write("&ensp;");
            }
            j = 0;
            while (j++<i*2-1) {
                document.write("*");
            }
            document.write("<br>");
        }
```

- 打印表格

```
        var i = 0,j;
        document.write("<table>");
        while(i++<9){
            j=0;
            document.write("<tr>");
            while(j++<9){
                document.write("<td>"+j+"*"+i+"="+j*i+"</td>");
            }
            document.write("</tr>");
        }
        document.write("</table>");
```

- 九九乘法表

```
	    var i = 0,j;
        document.write("<table>");
        while(i++<9){
            j=0;
            document.write("<tr>");
            while(j++<i){
                document.write("<td>"+j+"*"+i+"="+j*i+"</td>");
            }
            document.write("</tr>");
        }
        document.write("</table>");
```

- 深度遍历

```
调用对象名相同时
var obj={
	value:1,
	link:{
		value:2,
		link:{
			value:3,
             link:{
				value:4,
                  link:{
					value:5,
                      link:{
						value:6,
                           link:{
							value:7
							link:{};
                           }
                      }
                  }
             }
		}
	}
}
while(obj.link){
	console.log(obj.value);
	obj=obj.link;
}

调用对象不相同时
var obj={
	value:1,
	a:{
		value:2,
		b:{
			value:3,
             c:{
				value:4,
                  d:{
					value:5,
                      e:{
						value:6,
                           f:{
							value:7
							g:{};
                           }
                      }
                  }
             }
		}
	}
}
var arr = ["a","b","c","d","e","f","g"];
var i = 0;
var s = arr[0];
while(obj[s]){
    console.log(obj.value);
    obj=obj[s];
    i++;
    s=arr[i];
}
```

- 二叉树（以后再说）

```
  var tree={
      left:{
          value:1,
          left:{

          },
          right:{

          }
      },
      right:{
          value:2,
          left:{

          },
          right:{
              
          }
      }
  }
```

##### 	for

循环三要素：即表达式1，表达式2，表达式3
    	(循环变量赋初值，循环判定条件，循环增量）
循环体：需要重复执行的语句。

```
for（表达式1；判断表达式2；表达式3）
｛
		循环体；
｝
```

- `for(语句1;语句2;语句3){}` 语句3所在位置的语句块的含义是，一次循环执行完毕之后一定会要执行的语句，不一定是变量不断变化的语句

```
var i = 0,sum = 0;
for(i = 0;i++ < 100;sum += i);

var i = 0;						for(var i=0;i<100;i++){
while(i<100){						if(i===50) continue;
	if(i===50) continue;			console.log(i);
	console.log(i);				} //i++是每次循环完必执行的
	i++;
} //死循环,把i++放在if前面
	就不是死循环了
```

- 典型的死循环

```
for(;;){
}
```

for 应用：

- 深度遍历

```
var obj={
	value:1,
	link:{
		value:2,
		link:{
			value:3,
             link:{
				value:4,
                  link:{
					value:5,
                      link:{
						value:6,
                           link:{
							value:7
							link:{};
                           }
                      }
                  }
             }
		}
	}
}
for(;obj.link;obj=obj.link)
	console.log(obj.value);//一般用while
```

- 0-100之间所有的质数

```
for(var i = 2,j,bool;i<100;i++){
	for(j = 2,bool=true;j<i;j++){
		if(i%j===0){
			bool=false;
			break;
		}
	}
	if(bool) console.log(i);
}
```

- 打印表格

```
var row=10;
var col=10;
var str="<table>";
for(var i = 0;i<row;i++){
	str+="<tr>";
	for(var j=0;j<col;j++){
		str+="<td></td>"
	}
	str+="</tr>"
}
str +="</table>";
document.body.innerHTML+=str;
```

- 打印100-999之内的水仙花数

```
for(var i = 100,a,b,c;i<1000;i++){
	a=parseInt(i/100);
	b=parseInt(i/10)%10;
	c=i%10;
	if(a*a*a+b*b*b+c*c*c===i) console.log(i);
}
```

- 打印菱形（减少的用--，增多的用++）

```
var row = 10;
var col = 20;
for (var i = 0; i < row; i++) {
    if (i < 5) {
    	for (var k = row - i - 1; k >= 0; k--) {
        	document.write("&ensp;");
    	}
    	for (var j = 0; j < i * 2 - 1; j++) {
        	document.write("*");
    	}
	} else {
        for (var k1 = 0; k1 < i; k1++) {
            document.write("&ensp;");
        }
        for (var j1 = (row - i - 1) * 2; j1 >= 0; j1--) {
            document.write("*");
        }
    }
    document.write("<br>");
}
```

- 字符串的倒装

```
var str="abcdefghijklmnopqrstuvwxyz";
var s ="";
for(var i = str.length-1;i>=0;i--){
	s+=str[i];
}
console.log(s);
```

- for中break和continue

```
for(var i=0;i<10;i++){
	if(i===3) continue;
	if(i===5) break;
}

tag:for(var i=0;i<10;i++){
	for(var j=0;j<10;j++){
		if(j*i>50) break tag;
	}
}
```

- 注意当进行从大到小循环时，条件注意使用=的临界值问题
- 使用循环的时候，一定要尽可能避免循环定义变量
- 在双重循环时，不要在内层中判断外层变量或者改变外层变量
- 如果使用break时，不写跳出的label，它仅跳出当前层循环
- 循环是同步的,循环时不执行下面的代码
- 循环次数不能超过10亿次，循环不能嵌套太多，一般不超过2层
- 循环条件均会隐式转换为布尔值
- 六种循环中while相对来说效率比较高，递归循环的时间复杂度最低
- `document.body.innerHTML = str`会将body内原本的内容替换掉，将等号换成 += 就可以了

##### 	循环嵌套

```
for(var i=0;i<10;i++){
   for(var j=0;j<10;j++){
		console.log(i,j,i*j)
	}
}
```

#### break

- break语句会立即退出循环，强制继续执行循环后面的语句，结束本层循环。

```
var i = 0;
while(true){
	if(i>50) break;
	console.log(i);
	i++;
}
```

- 求0-100所有质数(除了1和本身之外，没有其他余数)

```
        var i = 1,j = 2;
        var bool;
        while(i++<100){
            j = 2;
            bool = true;
            while(j<i){
                if(i%j===0){
                    bool = false;
                    break;
                }
                j++;
            }
            if (bool) {
                console.log(i);
            }
        }
```

- 循环前增加id

```
        var i=0,j=0;
        wk:while(i++<10){
            j=0;
            while(j++<10){
                if (i*j>50) {
                    break wk;
                    //break 跳出到指定的id位置
                }
            }
        }
        console.log(i,j);
```

- 打印第一个水仙花数

```
        var i = 1,
          	j = 0,
         	n = 0;
        abc: while (j < 10) {
          n = 0;
          while (n < 10) {
            if (i * i * i + j * j * j + n * n * n === i * 100 + j * 10 + n)
              break abc;
            n++;
          }
          j++;
        }
        console.log(i * 100 + j * 10 + n); 
```

#### continue

- 当整个循环中遇到阶段性不需要执行的内容可以使用continue

- continue语句仅用于循环语句。虽然也是立即退出循环，但退出循环后会从循环的顶部继续执行，结束本次循环进行下一次

```
for (var box = 1; box <= 10; box++) {
	if (box === 5) continue;	//如果box是5，就退出当前循环
	document.write(box);
	document.write('<br />');
}
```

​		应用:

```
//stringObject.charCodeAt(index); 
可返回指定位置的字符的 Unicode 编码。
	index:表示字符串中某个位置的数字，即字符在字符串中的下标。
//String.fromCharCode(numX,numX,...,numX);
可接受一个指定的 Unicode 值，然后返回一个字符串。
	numX:一个或多个 Unicode 值，即要创建的字符串中的字符的 Unicode 编码。
//输出0123456789abcdef……zABCD……Z
    var i = 47;
    var str = "";
    while (i++ < 122) {
      if (i > 57 && i < 65) continue;
      if (i > 90 && i < 97) continue;
      str += String.fromCharCode(i);
    }
    console.log(str);
```

