## 对象

#### 对象创建

##### 构造函数创建法

```
var obj=new Object();
```

##### 字面量创建法

```
var obj={}；
```

##### 原型对象创建

```
var obj=Object.create({});
    Object.create(proto, [ propertiesObject ])
    proto对象原型
    propertiesObject 一组属性和值，该参数对象不能是 undefined，另外只有该对象中自身拥有的可枚举的属性才有效，也就是说该对象的原型链上属性是无效的。
    该方法可以针对已知对象创建新对象也可以创建一个空对象。关于原型链，我们在后面会详细讲解，因此本部分内容我们会在后面的继承中详细讲解。
```

#### 对象基础

- 中括号中的属性和方法必须是字符串，如果是变量，该内容必须是字符型变量。

```
	var a ="keys";
	var obj={
		name:"wk",
		//字符型key
		[a]:16,
		//变量型key
		5:10
	}
	//key如果不是字符串
	console.log(obj.name);
	console.log(obj.keys);
	console.log(obj.5);//报错，点语法拒绝使用非字符类型属性
	console.log(obj[5]);//在对象中key除了字符类型以外只能支持symbol类型，如果 Symbol 的参数是一个对象，那么就会调用 toString() 方法先将其转换为字符串。
```

- 对象的属性必须是字符串，否则不能使用点语法来获取
- 点语法只能获取属性名明确的字符串属性

```
var o ={
		a:1
	}
var o1={
		b:2
	}
	var arr[1,2,3];
	var arr1[4,5,6];
	obj[o]=10;
	obj[undefined]=20;
	obj[null]=30;
	obj[arr]=40;
	console.log(obj[o1]); //10
	console.log(o)；
	//变量型的key会使用toString()方法自动转成字符类型，数组除外（o和o1转换成字符类型都是[object Object]）
	//默认情况下，toString()方法被每个Object对象继承。如果此方法在自定义对象中未被覆盖，toString()返回 "[object type]"，其中type是对象的类型。
	console.log(obj); //▼object
						xxxx
	console.log(obj[o]===obj[o1]);//true
```

#### 对象的存储引用

- 对象存储在堆中，栈中存储对象的地址

- 对象打印中出现的数据问题

```
    var obj={
        a:1
    }
    console.log(obj);
    //只是打印了地址，然后运行obj.a=10
    //第一次输出▼object         刷新后输出▼{a: 1}
				a: 10					a: 10
    obj.a=10;
    
1、第一次运行结果

​	结果说明：第一次运行，在浏览器缓存中没有关于obj对象的缓存，在点击左上角的小三角的去获取a的值的时候，整个浏览器才会去堆中加载obj对象，所以第一行只有一个Object，没有任何别的信息可以输出，因为还没有获取，点击左边小三角查看信息的时候，这时候整个script已经执行完毕了，这个时候获取到的a的值就是最终的值，就是10

2、刷新之后

​	结果说明：再次刷新的时候，浏览器中已经有了obj的缓存，所以在第一行就会输出对象obj的相关信息，这个时候还没有去获取obj的值，仅仅是使用缓存中的值，所以第一行的时候a是1，但是点击三角获取obj信息的时候，堆中obj的a仍然是10
```

- JSON 将对象转换成字符串,这样比较准确

```
var str = JSON.stringify(obj);//对象转换为JSON格式的字符串
```

- JSON格式字符串

```
var s ='{"a":1,"b":2,"c":"wk","checked":true,"o":{"a":1}}'
```

- 将JSON格式字符串转换为对象

```
    var o =JSON.parse(s);
    console.log(o);
```

- 对象的引用关系问题

```
var obj={
    a:1
}
var obj1=obj;//将obj的地址赋给obj1
obj.a=100;
console.log(obj1.a);//obj和obj1的值都是引用地址，所以当改变对象的内容时，他们两个变量都是这个对象，输出100
	
例：
var o={a:1};
var o1=o;
o1.n=o={b:3};
console.log(o1,o);//{a:1,n:{b:3}}  {b:3}

var o={a:1};
var o1={a:1};
console.log(o===o1);//判断对象是否相等，仅判断地址，而不是判单对象里面的内容是否相等
console.log(JSON.stringify(o)===JSON.stringify(o1));//true 有漏洞，有可能会出错，如果一个对象里是有两个属性的，只是位置不一样而已，这样的方法就是错误的。
```

- 垃圾回收机制（面试题）

```
垃圾回收：
	在堆中的对象可能被若干个变量引用其地址，如果这个对象在后面的内容当中
不再使用，我们需要将堆中的这个对象清除，否则，不会被浏览器自动清除，这样就会造成内存的垃圾产生，当不断产生这种垃圾时，我们就把这种情况叫做内存泄漏。

如何处理内存泄漏：
	先创建每个对象的管理池，针对每个对象所引用它的变量做统一存储管理，如果需要清理该对象时，将引用他的所有变量设置为null，当内存上限达到峰值时，系统会通过垃圾回收车将这些堆中无引用的对象全部清除回收，这就是垃圾回收机制。
```

#### 对象遍历

for in

```
var obj={
	a:1,
	b:2,
	c:3,
	d:4,
	e:5
}
for(var prop in obj){
	console.log(prop,obj[prop]);
	//prop打印的是属性名
	//obj[prop]打印的是属性值
}
```

对象的属性时散列的，遍历的时候是通过我们添加属性的先后顺序遍历的

```
//如果是				打印出来：
var obj={				var obj={
	c:3,					a:1,
	a:1,					b:2,
	b:2,					c:3,						 
	d:4,					d:4,
	e:5						e:5
	f:{						f:{
		a:6						a:6
	}						}
}						}
console.log(obj);
```

对象的复制（浅拷贝）

- 如果对象中只有属性值，则复制的对象没有引用关系；
- 如果对象中有对象，则对象中的对象属性有引用关系。

```
var obj={
	a:1,
	b:2,
	c:3,
	d:4,
	e:5
	f:{
		a:6
	}
}
var obj1 = {};
for(var prop in obj){
	obj1[prop] = obj[prop];
}
obj.f.a=10;//引用的地址不同，obj1.a的值不改变
console.log(obj1);
```

对象的复制（深拷贝）

- 可以完成对象的深度复制，但是仍然存在很多问题：JSON的方法不可以将对象中的方法进行转换，用这种方法转换的对象方法均被忽略

```
var obj={
	a:1,
	b:2,
	c:3,
	d:4,
	e:5
	f:{
		a:6
	}
}
var obj1=JSON.parse(JSON.stringify(obj));
obj.f.a=100;//obj1的值不改变
console.log(obj1);
```

- 对象中的原型属于不可枚举属性

#### 删除对象中的属性

- delete 不能删除window下的属性和方法

```
var obj={a:3,b:4}
delete obj.a;
```

## 函数

#### 函数基础

1、函数是一个对象，存储在堆中

2、函数的创建

第一种方式（普通函数创建）

```
    function fn1(arg1,arg2)
    {
        // 函数的语句块
        console.log("a");
    }
```

- 这种普通函数创建，在script被执行时，就放在堆中，并且在栈用以函数名作为变量引用堆中这个函数地址

- 函数在创建时就创建这个函数名的变量，因为它是全局的，所以就会被污染覆盖，覆盖前仍然可以执行当前函数，覆盖后，函数不能够执行了

- 如果函数中没有使用return关键词，函数返回一个underfined值

```
     function fn1(arg1,arg2){console.log("a")}
     console.log(fn1());
     //输出a和undefined
     
     console.log(fn1);
     //会打印整个函数内容
     console.dir(fn1);
     //以对象形式打印函数
     
     支持给函数添加属性
     fn1.a = 3;
```

- 函数本身就是一个对象，所以可以给函数添加属性，同时也具备引用关系

```
fn1.a=10;
var fn = fn1;//函数是对象，因此拥有引用关系
fn();
```

第二种方式（匿名函数创建）

```
fn2();//这里调用会报错
var fn2 = function(){
}
fn2();//此时才会被调用
```

- 匿名函数创建，创建好的匿名函数赋值给fn2这个变量
- 变量什么时候定义，这个变量才能栈中产生，才可以被调用

- 自执行函数

```
(function(){
	console.log("aa");
	//会自动执行一次，以后永远不能再调用
})()
```

​		应用：

```
var bn = document.getElementById("bn");
bn.onclick = function(){
	console.log("aa");
	bn.onclick = null;
}//只能点击一次

构造函数创建函数
//构造函数创建，每个参数都必须是字符串
//除了最后一个参数是函数的语句块以外，前面所有的参数都是该函数的参数
var fn = new Function("a","b","console.log(a+b)");
```

第三种方式（构造函数创建）

```
var fn = new Function("a","b","console.log(a+b)");
```

- 构造函数创建，每个参数都必须是字符串

- 除了最后一个参数是函数的语句块以外，前面所有的参数都是该函数的参数
- 优点：所有的字符串都可以转换，可以动态接收服务端传过来的代码和参数，转换后进行执行，可以使得前端的代码不固定，通过后端动态生成

#### 函数参数

1. 参数是指由外部传入到函数中的变量，仅作为变量使用，但是该变量可以是任何内容，包括函数。
2. 被传入的参数作为私有变量使用，可以被覆盖掉。
3. 外部传入的参数可以节省全局变量的定义，甚至保证函数中的部分变量的独立性。
4. 参数的作用：使得函数能够在不同情况下解决不同问题，使得函数能够处理一类问题，而不是一个
5. 在设计函数的时候，尽量不要让函数内部和外部有关联，尽量让函数内部是一个独立的个体
6. 函数不要太复杂，每个很小的功能都可以抽象出来做一个单独的函数
7. 因为js是一种弱类型语言，因此不能对函数的参数约束类型，这就会造成，因为使用者输入的参数不符合要求而造成代码出错
8. ES5版本中，js中参数不能设置初始值，不填写参数值，就默认为undefined
9. 形参和实参的定义
10. js中实参是按照形参顺序一一赋值个形参的，如果实参数量小于形参数量，后面的形参的值为undefined

应用：

​		打印表格

```
	function createTable(row, col) {
        var str = "<table>";
        for (var i = 0; i < row; i++) {
          str += "<tr>";
          for (var j = 0; j < col; j++) {
            str += "<td></td>";
          }
          str += "</tr>";
        }
        str += "</table>";
        document.body.innerHTML += str;
      }

      createTable(3, 10);
      createTable(5, 10);
      createTable(6, 8);
```

​		计算加减乘除

```
	  function fn1(a,b){
            var s=a+b;
            console.log(s);
      }
      function fn2(a,b){
            var s=a-b;
            console.log(s);
      }
      function fn3(a,b){
            var s=a*b;
            console.log(s);
      }
      function fn4(a,b){
            var s=a/b;
            console.log(s);
      }
      fn1(3,5);
      fn3(3,5); 
或者
	function fns(a,b,type){
        var s;
          switch(type){
              case "+":
              s=a+b;
              break;
              case "-":
              s=a-b;
              break;
              case "*":
              s=a*b;
              break;
              case "/":
              s=a/b;
              break;
          }
          console.log(s);
      }
      fns(3,5,"*");
```

##### arguments

什么时候使用:

- 定义函数时没有定义参数
- 如果实参数量大于形参数，使用arguments
- arguments只能出现在函数语句块中
- 用于当前函数的参数不固定数量

arguments中的属性

```
function fn1(){
    //console.log(arguments.callee); 当前函数
    //console.log(arguments.callee.name); 当前函数的名字
    //console.log(arguments.callee.caller); 调用当前函数的外部函数，返回函数代码
    }
```

- 实参的长度小于形参的长度：`arguments.calee.length < arguments.length`

- 函数的长度fn.length是指形参的长度，arguments的长度是指实参的长度

应用：

- 求输入参数的和

```
	function sum(){
        var s = 0;
        for(var i=0,i<arguments.length;i++){
            s+=arguments[i];
        }
        console.log();
    }
```

- 求输入参数的最大值

```
		function max() {
            if(arguments.length===0) return "没有值";
            if(arguments.length===0) return arguments[0];
            var max = arguments[0];
            for(var i=1;i<arguments.length;i++){
                max=max>arguments[i] ? max : arguments[i];
            }
            return max;
        }
        var x = max(1,4,7);
        console.log(x);
```

- 让自执行函数再执行一次 

```
    var i = 0;
    (function(){
        i++;
        if(i<5) arguments.callee();
    })(); //当i<5再执行一次
```

##### 变量的作用域

1、局部变量和全局变量

- 变量只能在局部中使用，因此叫做局部变量
- 在任何地方都可以使用的变量，叫做全局变量
- 被定义在函数内部的变量，使用范围仅在函数内部，并且当前函数执行完成以后，这个变量会被销毁，下一次这个函数在执行时，会重新定义这个变量，并且变量不能被保存在函数执行完成后还能使用。

2、局部变量优先：只要函数中有var定义，这个变量就一定是局部变量，并且局部优先，形参就相当于被定义好的局部变量，重复定义的局部变量（形参也是一种定义）不赋值不起作用

```
var a = 5;
function b(){
	console.log("function    "+a);//a是undefined，局部变量优先，但是赋值在后
	var a = 4;
	console.log("function    "+a);//a是4
	
    // console.log(a+window.a);ES6中完全禁止
}
b();
console.log(a);//a=5没有被b函数修改
```

- 函数都会被优先解释和编译，跟书写位置没有关系

```
var a;
function a(a){
	console.log(a);
	var a;
	console.log(a);
	a = 10;
	console.log(a);
}
a(6);//可以执行
a = 100;
a(6);//报错
```

- 变量提升只会提升变量名的声明，而不会提升变量的赋值初始化，同理，函数声明也是如此。
- 函数提升的优先级大于变量提升的优先级，即函数提升在变量提升之上。

```
原来的代码：
console.log(foo);
foo();//可以执行
var foo=10;
foo();//foo已经被赋值为一个变量，无法执行foo为函数
console.log(foo); 
function foo(){
  var a;
  console.log(a);
  a=12;
  console.log(a);
}
console.log(foo);

实际的执行顺序：
function foo(){
  var a;
  console.log(a);
  a=12;
  console.log(a);
}
var foo;
console.log(foo);//打印函数
foo();//underfined  12
foo=10;
foo();//由于这里报错，foo已经被赋值，找不到这个函数，下面的都不会被执行
console.log(foo);
console.log(foo);
```

面试题：

```
var a = 10;
function fn(){
	//如果当前函数内没有定义局部变量时，这里调用的是全局变量
	console.log(a);//10
}
fn();


var a = 10;
function fn(){
	var a;
	console.log(a);//遵照局部变量优先原则，输出undefined
}
fn();


var a = 10;
function fn(){
	console.log(a);//仍然遵照局部变量优先原则，输出underfined
	var a; // var a=4;还是打印undefined
}
fn();


//在函数中只要看到使用var定义的变量，这个变量就一定局部变量，而且这个变量被优先
var a = 10;
function fn(){
	console.log(a);//10，这里没有使用var，当前a是全局的
	a = 4;
}
fn();
console.log(a); //4
//函数内部如果没有var声明变量，直接赋值的话，会自动创建变量，此时变量是全局的


var a = 10;
function fn(a){
	//当在函数中设置了参数，那么就相当于，这个参数就是被定义好的局部变量
	console.log(a);//5
}
fn(5);


var a = 100;
function fn(a){
	console.log(a);//6
	var a;//因为参数本身就是局部变量，所以重新定义不赋值不起作用
	console.log(a);//6
	a=10;
	console.log(a);//10
}
fn(6);


var a = 100;
function a(a){
	console.log(a);
	var a;
	console.log(a);
	a=10;
	console.log(a);
}
a(6);//a is not a function


var a ;//只是声明了，赋值之后才会变量污染
function a(a){
	console.log(a);
	var a;
	console.log(a);
	a=10;
	console.log(a);
}
a(6);//可以执行
a=100;
a(6);//报错，覆盖了


var a;
function a(a，a){
	console.log(a);//7
	var a;
	console.log(a);//7
	a=10;
	console.log(a);//10
}
a(6，7);//可以执行
a=100;
a(6);//报错


var a={
	a:function(a){
		var a;
		console.log(a);
	}
}
a.a(5);//5


//局部变量只属于此函数的
function fn(f){
	var x=20;
	f(x);//相当于执行了fn1();
}
function fn1(x){
	console.log(x);//20,如果没有传x，则不是20
}
fn(fn1);
```

面试题：

​		函数中的局部变量不会向下传递，在函数中调用函数，不会将当前函数的局部变量传递到当前函数调用的函数中

```
var x = 10;
function fn() {
	console.log(x)
}
function show(f) {
	var x = 20
	f()
}
show(fn) ;
//10
```

面试题：

​		只要变量在函数当中有声明了，就会把声明提到最前面，不管这个声明在什么位置上，就算是在分支和循环中，也会提到最前面

```
var name = 'World!';
(function () {
	if (typeof name === 'undefined') {
		var name = 'Jack'
		console.log(name)
	} else {
		console.log(name)
	}
})()

//输出Jack
```

面试题：

```
var num1=1;  
function testf1(){
	num1=2;  
	alert(num1);
}
function testf2(){ 
	alert(num1); 
}   
testf1();  
testf2();
//输出结果为2,2

原因：在运行testf1的时候，因为没有定义局部变量，所以去找num1的全局变量，将全局变量改为2，所以后面再访问全局变量的时候，num1的值为2
```

#### length

arguments.callee.length

arguments.length

```
function fn(a,b){
	if(arguments.callee.length<arguments.length)//形参长度小于实参长度
	console.log(arguments.length);//实参的长度
}
console.log(fn.length);//形参的长度
```

清除函数

```
fn=null;
```

函数属性删除

```
function fn(){

}
delete fn(){

}//删除函数的属性有效
delete window.fn;//无效
```

#### return

- 函数在执行时，将返回函数中return内容
- 如果return 后没有内容或者没有return，返回一个undefined

```
function fn(){
    return 1;
}
function fn1(){
    return 2;
}
        
var s=fn();//1
console.log(s);

var s=fn()+3;//4
var s=fn()+fn1();//3
```

#### 函数返回的作用

##### 返回函数的局部变量

```
function fn(){
	var a = 1;
	a+=3;
	return a;
} //4

function fn(_name,_sex){
	/* var obj={
		name:_name,
		sex:_sex
	   } 
	   return obj;
	*/ //局部变量没有用到，会造成浪费
	return {
		name:_name,
		sex:_sex
	}
}
var obj = fn("wk","男"); //▼Object
                            name: "xietian"
                            sex: "男"


function fn(){
   var fn1=function(){
        console.log("aa");
    }
    return fn1;
}
或
function fn(){
    return function(){
        console.log("aa");
    }
}
var f=fn();  //返回嵌套的整个函数代码
f();//aa
```

##### 返回参数

```
function fn(a,b){
	a+=b;
	return a;
}
var a = 10;
var b = 20;
a = fn(a,b);
console.log(a);//30
fn(a,b);
console.log(a);//10


function fn(obj){
	obj.a=10;
	return obj;
}
var obj={
	a:1;
}
fn(obj);
console.log(obj);//a:10,会改变
var obj1=fn(obj); //返回的obj的地址数字赋给obj1
console.log(obj===obj1); //true
```

##### 跳出，切断，不继续执行

```
function fn(a,b){
	if(isNaN(a) || isNaN(b)) return;
	console.log("是数值");
}
fn(3,5);
```

应用：

- 加减乘除

```
var sum = fn(a,b,"*");
function fn(a,b,type){
	if(isNaN(a) || isNaN(b)) return "错误的数字";
	switch(type){
		case "+":return fn1(a,b);
		case "-":return fn2(a,b);
		case "*":return fn3(a,b);
		case "/":return fn4(a,b);
		default:return "错误的符号";
	}
}
function fn1(a,b){
	return a+b;
}
function fn2(a,b){
	return a-b;
}
function fn3(a,b){
	return a*b;
}
function fn4(a,b){
	if(b===0) return "错误除数";
	return a/b;
}
```

- 输入阿拉布数字，转换为中文数字

```
var str="零一二三四五六七八九十";
function changeCN(num){
	if(isNaN(num)) return "这不是一个数字";
	if(num>=100 || num<0) return "数字不在范围内";
	num=parseInt(num);
	if(num<11) return str[num];
	if(num<20) return "十"+str[num%10];
	if(num%10===0) return str[(num/10)]+"十";
	return str[parseInt(num/10)]+"十"+str[num%10];
}
console.log(changeCN(96));//九十六
```

#### 函数的运行过程

​		函数执行中执行其他函数，另一个函数中的内容执行完成后才会继续执行，当需要并列执行多个时，我们可以在一个函数中统一调配执行的顺序

```
function fn1(){
	console.log("a");
	fn2();
	console.log("c");//fn2()运行完成后，再运行
}
function fn2(){
	console.log("b");
}
function fn3(){
	console.log("e");
	return console.log("e");//同上，没区别，跳出的只是fn3()
}
function fn4(){

}
function fn5(){

}
fn1();

或者

function fn1(a){
	if(a===1) return fn2();
	if(a===2) return fn3();
	if(a===3) return fn4();
	if(a===4) return fn5();
}
function fn2(){
	console.log(1);
}
function fn3(){
	console.log(2);
	return 10;
}
function fn4(){
	console.log(3);
}
function fn5(){
	console.log(4);
}
var s = fn1(2);
console.log(s); //2 10


var s = 0;
switch(a){
	case 1:s+fn2();
	case 2:s+fn3();
	case 3:s+fn4();
	case 4:s+fn5();
}
function fn2(){
	console.log(1);
	return 10;
}
function fn3(){
	console.log(2);
	return 20;
}
function fn4(){
	console.log(3);
	return 30;
}
function fn5(){
	console.log(4);
	return 40;
}
var s=fn1(2);//2 3 4 90
```

#### 回调

将一个函数以参数的形式传入到另一个函数中，并在那个函数执行

```
function fn1(fn){
	fn();
}
function fn2(){

}
fn1(fn2);
```

1、回调一般用于当处理某家事情需要等待时，设置回调

- setTimeout(超时执行的函数，超时时间（毫秒），执行函数的参数) 返回一个id数值，异步，并用clearTimeout()清除
- setInterval(一定时间执行的函数，超时时间（毫秒）)会根据时间一直执行,异步，并用clearInterval()清除

```
console.log("a");
var id = setTimeout(fn,2000,5);//异步，一定时间后处理问题
function fn(n){
	console.log(n);//过两秒后执行打印5
	clearTimeout(id);//清除这个超时函数，不清除就一直在堆中
}
console.log("b");//打印a b 5


var id = setInterval(fn,2000); 
var num = 0;
function fn(){
	num++;
	console.log("aa");
	if(num>3) clearInterval(id);
}
```

2、当不需要关系具体后续需要处理的事情时，设置回调

```
function fns(a,b,fn){
	if(isNaN(a) || isNaN(b)) return "错误的数据";
	return fn(a,b);
}
function fn1(a,b){
	return a+b;
}
function fn2(a,b){
	return a-b;
}
function fn3(a,b){
	return a*b;
}
function fn4(a,b){
	if(b===0) return "错误除数";
	return a/b;
}
var s = fns(3,5,fn3);
console.log(s);


//红绿灯
var id = 0;
function setLight(){
    arguments[0](arguments[1],arguments[2]);
    //红（黄，绿）
}
function redLight(fn,fn1){
                //(黄，绿)
    clearTimeout(id);
    console.log("红灯");
    id = setTimeout(fn,2000,fn1,arguments.callee);
            //(黄，绿，红)
}
function yellowLight(fn,fn2){
                    //(绿，红)
    clearTimeout(id);
    console.log("黄灯");
    id = setTimeout(fn,2000,fn2,arguments.callee);
            //(绿，红，黄)
}
function greenLight(fn,fn2){
            //(红，黄)
    clearTimeout(id);
    console.log("绿灯");
    id = setTimeout(fn,2000,fn2,arguments.callee);
            //(红，黄，绿)
}
setLight(redLight,yellowLight,greenLight);


//回调函数完成循环局部传参返回值
//加
function fn1(fn, i, sum) {
	if (i === undefined) (i = 0), (sum = 0);
	i++;
	if (i > 100) {
		return sum;//此时返回值是返回上一个函数
	}
		return fn(arguments.callee, i, sum);//如果没有加return，sum则输出undefined
}

function fn2(fn, i, sum) {
	sum += i;
	return fn(arguments.callee, i, sum);//如果没有加return，sum则输出undefined
}
//乘
function fn1(fn, i, sum) {
	if (i === undefined) (i = 1), (sum = 1);
	i++;
	if (i > 100) {
		return sum;//此时返回值是返回上一个函数
	}
		return fn(arguments.callee, i, sum);
}
function fn3(fn, i, sum) {
	sum *= i;
	return fn(arguments.callee, i, sum);
}

var sum = fn1(fn2); //5050
var sum = fn1(fn3); //9.33262154439441e+157
console.log(sum);
```

#### 递归

满足以下三个特点就是递归：

1. 函数自己调用自己
2. 一般情况有参数
3. 一般情况下有return

递归的方法：

1. 首先去找临界值，即无需计算，获得的值。
2. 找这一次和上一次的关系
3. 假设当前函数已经可以使用，调用自身计算上一次

```
计算1~n的和
sum(100) = sum(99) + 100;
sum(n) = sum(n - 1) + n;

function sum(n){
    if(n == 1){
        return 1;
     }
    return sum(n - 1) + n;
}
console.log(sum(100));
```

函数内执行当前自身函数

```
var i = 0;
function fn1(){
	i++;
	if(i<3) fn1();
	console.log(i);
}
fn1();//第一次③3  刷新后3 3 3

运行顺序细节：
function fn2(){
    i++;	//1
    if(i<3) fn3();
    console.log(i);
}
function fn3(){
    i++;	//2
    if(i<3) fn4();
    console.log(i);
}
function fn4(){
    i++;	//3
    if(i<3) fn1(); //不被执行
    console.log(i);
} 
```

根据内存大小设置递归上限的次数，如果递归次数太多，就会堆栈上限溢出

```
var i=0;
fn1();

function fn1(){
    i++;
    if(i<20000) fn1();
    // console.log(i);
}
```

标签id的广度深度遍历



```
function getDOMObj(parent,obj){
    obj=obj || {};
    parent=parent || document.body;
    if(parent.id) obj[parent.id]=parent;
    for(var i=0;i<parent.children.length;i++){  //广度
        getDOMObj(parent.children[i],obj);  //深度
    }
    return obj;
}
var obj=getDOMObj();
console.log(obj);
```

对象的深复制

```
function cloneObj(obj,target){
    target=target || {};
    for(var prop in obj){
        if(typeof obj[prop]==="object" && obj[prop]!==null){
            target[prop]={};
            cloneObj(obj[prop],target[prop]);//属性名的复制
        }else{
            target[prop]=obj[prop]; //如果不是对象,比如a:1
        }
    }
    return target;
}

var obj1=cloneObj(obj);
obj.c.a=10;
obj.d.b.b.c=100;
console.log(obj1); //obj1的属性值不改变
```

## 数组

#### 数组的创建

- 有序列表存储若干个无序的元素，紧密型结构
- 将元素放在列表中的第几位，从0开始计算，这个位置就是下标。又叫做索引值
- 元素被存储在列表中，这个数据就是元素，简称元
- 从列表中获取这个元素的方标，使用 数组名[下标]就可以得到这个元素，把这种方法叫做下标变量

```
var arr = [];
arr[0]=10;
arr[3]=20;
//arr[3] 下标变量  3就是下标  20就是元素  arr讲就是数组
console.log(arr[3]);//20
console.log(arr);//[10, empty × 2, 20]
```



字面量创建数组

```
var arr = [1,"a",true,undefined];
var arr=[1,2,3,4]; //一般把相同类型的数据放在一起
var arr[]; //创建空数组
//因为js是弱类型语言，因此数组比较随意，可以任意扩张，不需要限定它的长度，也无法限定长度
```

构造函数创建法

```
var arr = new Array(4,5,6,7,8);
var arr = new Array(5);
var arr = Array(5);//意义同上，但是建议new一个
//如果构造函数创建数组时，仅有一个参数且这个参数是一个大于0的正整数，这个数就是这个新数组的长度，并且没有元素。如果负数或者小数，就会报错。如果时非数值类型，就会将这个元素放在数组的第0位
```

对象创建法

```
var arr = new Object([1,2,3,4]);

console.log(typeof arr); //object
console.log(arr.constructor===Array); //true,constructor构造函数,最保险的方法
console.log(Array.isArray(arr)); //true,ES6之后的浏览器才支持
console.log(String(arr)); //1 2 3 4
console.log(String(arr)!=="[object Object]"); //true
```

数组也是对象

```
var arr = [1,2,3,4];
var arr1=arr;
arr[0]=10;
console.log(arr1); //数组也是引用类型，引用地址赋值
//数组在强转或者隐式转换为字符串时，都会转换为数组的元素连接

console.log([]===[]); //false,对象和对象引用地址数值不同
console.log([]==[]); //false，同上
console.log(![]==[]); //true
console.log(![]); //![]会转为布尔值，也就是false，[]与布尔值比较，双方都转成数值
console.log([]==""); //true
console.log([]==false); //true
console.log([]==0); //true
```

#### 对象和数组的区别

对象：

1、对象是一种松散型结构，对象是键值对存储，当删除一个元素时，对象的其他内容不会发生改变

2、对象是没有元素的个数，也就是对象长度

3、对象中不知道存储了多少个元素，插入和删除不会影响其他数据，插入和删除时间复杂度极低，因为对象通过key去一一对应存储一个值，所以获取时，只根据key去取值就可以了

4、对于对象来说，因为每个数据都是独立存在的，不存在关联关系，更不能排序，所以不能因关联关系找到对应的值

数组：

1、数组时紧密型结构，只用下标存储对应的值，当删除一个元素时，因为紧密结构的关系，就会将后面的元素向前递进

2、数组是有长度

3、数组中可以知道存储了多少元素，插入和删除时，都会影响数组的位置和结构，因此插入和删除都会影响数组的运行效率时间复杂度较高，因为数组的存储时依靠下标的，所以如果需要查找一个值，就需要遍历数组的每个元素，以达到找到目标元素。

4、数组在使用时，因为是紧密型结构，我们可以根据上一个内容找到与其相关联的元素，例如我们可以利用数组排序，找到一个最小值，还可以迅速找到第二位最小值。

#### 数组的长度

- `arr.length`就是长度，数组中元素的个数
- 数组的长度是一个可读可写的属性
- 如果数组的长度修改比原来的长度小，就会把对应多出来的元素删除

```
var arr=[1,2,3,4];
arr.length=3;
console.log(arr); //1,2,3
arr.length--;//删除最尾部的一个元素
arr.length=0; //删除数组中所有元素
arr.length++; //在数组尾部添加一个空元素 //1，2，3， ，
```

- 数组的长度比数组的最大下标值大1

```
arr[arr.length]=5; //在数组的尾部增加一个元素5
```

- 如果数组下标大于数组的长度时，就会在对应的下表位增加元素，中间增加空元素

```
var arr=[1,2,3,4];
arr[10]=100;
console.log(arr);
打印结果：Array(11)
            0: 1
            1: 2
            2: 3
            3: 4
            10: 100
            length: 11
```

#### 数组的遍历

for

```
var arr=[1,2,3,4];
arr[10]=100;
for(var i=0;i<arr.length;i++){
	console.log(i,arr[i]);
	//打印结果：
	0 1
	1 2
	2 3
	3 4
	4 undefined
	5 undefined
	6 undefined
	7 undefined
	8 undefined
	9 undefined
	10 100
	
	console.log(arr[i]===undefined); //如果是空值，返回true
	console.log(i in arr); //判断是否有数值，有的话返回true，与上相反
	//可以判断对象中这个key对应的值是否存在，在数组中下标就相当于对象中key，就可以判断它的对应值是否存在
}
```

for in

```
var arr=[1,2,3,4];
arr[10]=100;
arr.a=10;
arr.b=20;
for(var index in arr){
	console.log(index,arr[index]);
	打印结果：
	0 1
	1 2
	2 3
	3 4
	10 100
	a 10
	b 20
}
```

for与for in的区别

- 数组使用for循环遍历，会将所有下标遍历，不遍历数组的对象属性，但是会遍历到空元素，遍历时下标都是数值
- 数组使用for in循环遍历，会将所有的可枚举属性遍历（不可枚举属性有原型函数），如果该属性没有值就不遍历，例如数组中下标为空元素的，就不会被遍历，但是数组的对象属性会被遍历，遍历时都是将下标转换为字符串

#### 数组的方法

数组的两个方法形成栈结构：

##### push()

格式：数组.push(参数1, 参数2...);

功能：可以数组的末尾添加若干个元素。

返回值：插完元素以后数组的长度


```
var arr = [1,2,3,4];
vra len = arr.push(5,6,7,8);
console.log(arr);	// 8
```

​		循环给尾部添加若干个元素

```
var arr = [1,2,3,4];
while(arr.push(1)<10);
console.log(arr);	//[1,2,3,4,1,1,1,1,1,1]

var arr = [];
while(arr.push({})<10);
arr[0].a=10;
console.log(arr);	//数组中对象的引用关系不变
```

​		push重构

```
function push(arr){
    for(var i=1;i<arguments.length;i++){
        arr[arr.length]=arguments[i]; //给arr尾部加入元素
    }
    return arr.length;
}
var arr=[];
var len=push(arr,1,2,3);
console.log(len,arr);
```

##### pop()

格式：数组.pop()

参数：没有参数

返回值：删除的元素

功能：从数组末尾删除一个元素

```
var arr = [1,2,3,4];
var element = arr.pop();
console.log (element,arr);	//4	[1,2,3]
```

​		循环给尾部删除若干个元素

​		1、不能用pop删除，如果遇到空元素，会打印undefined；如果数组为空，返回空值，也会打印undefined

```
var arr = [1,2,3,4];
while(arr.pop()!==3);	//已经把4和3删除了
console.log(arr);	//[1, 2]
```

​	2、如果数组中存储的是对象，我们必须将所有的对象引用全部设为null

```
while(arr.length>0){
   arr[arr.length-1]=null;
   arr.pop();
}
arr.length=0;

//这种效率更高 
for(var i=0;i<arr.length;i++){
   arr[i]=null;
}
arr.length=0;
```

​		错误示范

```
var arr=[1,3,3,6,8,2,3,5,6,3,7,9,8,3,6,7,3,8,9];
for(var i=0;i<arr.length;i++){
    arr.pop();
}
console.log(arr); //删除到一半的时候就停止了，因为arr.length会改变
```

​		pop重构

```
function pop(arr){
    var elem=arr[arr.length-1];
    if(arr.length>0) arr.length--;	//如果没有元素，返回空数组
    return elem;
}
```

数组方法的形成的队列结构：

##### shift()

格式：数组.shift()

参数：没有参数

功能：从数组的头部删除一个元素

返回值：删除的元素


```
var elem=arr.shift();
```

​		shift重构

```
function shift(arr){
    var elem=arr[0];
    for(var i=1;i<arr.length;i++){
        arr[i-1]=arr[i];		//往前移项
    }
    if(arr.length>0) arr.length--;	//每运行一次，数组减少一个元素
    return elem;
}

var arr=[1,2,3];
var elem=shift(arr);
console.log(elem,arr);//1 [2,3]
```

##### unshift()

格式：数组.unshift(参数1, 参数2...)

功能：从数组的头部插入若干个元素

返回值：插完元素以后数组的长度

```
var len= arr.unshift(5,6)
```

​		unshift重构

```
移项实现
function unshift(arr){
    var len=arguments.length-1;
    for(var i=arr.length-1;i>=0;i--){
        arr[i+len]=arr[i];	//将数组向后移项
        arr[i]=null;	//有引用关系
    }
    console.log(arr);	//[null, null, null, 1, 2, 3]
   for(var j=1;j<arguments.length;j++){
       arr[j-1]=arguments[j];
   }
   return arr.length;
}

定义空数组实现
function unshift(arr){
    var arr1=[];
    for(var i=0;i<arr.length;i++){
        arr1[i]=arr[i];		//没有引用关系,[1,2,3]
    }
    arr.length=0;	//原数组清空
    for(var j=1;j<arguments.length;j++){
        arr[j-1]=arguments[j];		//将参数赋给arr，[4,5,6]
    }
    var len=arr.length;
    for(var k=0;k<arr1.length;k++){
           arr[len+k]=arr1[k];
           //或者
           arr[arr.length]=arr1[k];
    }
    return arr.length;
 }
 
var arr=[1,2,3];
var len=unshift(arr,4,5,6);
console.log(arr,len);
```

[注] 以上四个方法，操作后原数组的引用关系不变

##### join()

格式：数组.join(字符串)

参数：字符串，如果没有连接符，默认值以逗号连接

功能：将数组中的元素，用传入的拼接符，拼接成一个字符串

返回值：拼接好的字符串，原数组不变

```
var arr = [1,2,3,4];
var str=arr.join("*");
console.log(str);	//1*2*3*4
```

​		join重构

```
function join(arr,separator){
    if(separator===undefined) separator=",";
    separator=String(separator);
    var str="";
    for(var i=0;i<arr.length;i++){
       if(i!==arr.length-1) str+=arr[i]+separator;
       else str+=arr[i];
    }
    return str;
}
var arr = [1,2,3,4];
join(arr,"*");
console.log(str);
```

##### concat()

格式：数组.concat(数组，参数1, 参数2...)

功能：连接若干数组或者元素生成一个新数组

返回值：返回新数组，原数组不变，没有引用关系

[注] 就算传入是数组，数组中元素中的元素要单独拆出来再进行合并

```
var arr=[1,2,3,4];
var arr1=arr.concat([5,6,7],[8,9,0]);	//[1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
var arr1=arr.concat(5,6,7,8,9);	// [1, 2, 3, 4, 5, 6, 7, 8, 9]
var arr1=arr.concat();	//[1, 2, 3, 4]
arr[0]=10;	//arr1不改变，没有引用关系
console.log(arr1);
```

​		concat重构

```
定义空数组实现
function concat(arr){
    var arr1=[];
    for(var i=0;i<arr.length;i++){
        arr1[i]=arr[i];		//将arr中元素赋值给arr1
    }
    if(arguments.length===1) return arr1;
    for(var j=1;j<arguments.length;j++){
        if(arguments[j]!==null && arguments[j].constructor===Array){
            for(var k=0;k<arguments[j].length;k++){
                arr1[arr1.length]=arguments[j][k];	//参数第J个的元素值
            }
        }else{
            arr1[arr1.length]=arguments[j];
        }
    }
    return arr1;
}
var arr=[3,4,5];
var arr1=concat(arr,""); //[3, 4, 5, ""]

console.log(arr1);
```



##### slice()

格式：数组.slice(strat,end);	[start,end)

功能：可以基于当前数组获取指定区域元素[start,end)，提取出元素生产新数组

返回值：生成新的数组，原数组不变，没有引用关系

```
var arr=[1,2,3,4];
var arr1=arr.slice(2);//从第二项复制到尾部所有元素
var arr1=arr.slice(0);//复制数组
var arr1=arr.slice();//复制数组
var arr1=arr.slice(-2);//从后向前数第2个元素到尾部的所有元素复制
var arr1=arr.slice(1,2); //从第一项复制到第二项，不包括结束这一项
console.log(arr1,arr);
```

​		slice重构

```
定义空数组实现
function slice(arr,start,end){
    if(start===undefined) start=0;	//如果start是undefined，设置为0
    if(end===undefined) end=arr.length;	//如果end是undefined，设置为数组长度
    start=Number(start);
    end=Number(end);
    if(!isNaN(end) && isNaN(start)) start=0;	//比如（"a",1），设置start为0
    if(isNaN(start)) return [];		//start不是数值，则返回空数组
    if(start<0) start=arr.length+start;		//如果start是负数
    if(end<0) end=arr.length+end;		//如果end是负数
    var arr1=[];
    for(var i=start;i<end;i++){
        arr1[i-start]=arr[i];
    }
    return arr1;
}

var arr=[2,3,4,5];
console.log(arr.slice(true,"3"));
var arr1=slice(arr,true,"3");
console.log(arr1);
```

##### splice()

格式：数组.splice(start，length，参数1，参数2...)

参数：start 开始截取的位置

​			length 截取的元素的长度

​			第三个参数开始：在start位置，插入的元素，数组算一个元素

返回值：截取下来的元素组成的新数组，原数组改变

1、增加 	splice(start, 0, ele1, ele2, ...)

将数组中从第几位开始删除多少个元素，并且返回被删除的元素组成的新数组

2、删除 

将数组中从第几位开始删除多少个元素，并且返回被删除的元素组成的新数组

```
splice(start, length)	
splice(1)	从第一位删除到尾部
splice(-1)	从倒数第一为删除到尾部
splice()	没有删除并返回空数组
splice(0)	将一个数组的所有元素转移到另一个数组
splice(-3,2)	从倒数第3个元素向后删除2个元素
```

3、修改（先删除，再删除）	splice(start, count, ele1, ele2, ...)

将数组中从第几个位开始删除多少个元素后，并且在该位置插入新的若干元素，返回删除元素组成的新数组

[注] 这个方法实现需要耗费大量时间

```
var arr1=arr.splice(1,2,-2,-3);
//从第一位开始向后删除两个元素，并且在该位置插入-2和-3，替换，并且返回被删除两个元素组成的数组
var arr1=arr.splice(1,arr.length,0,-1,-2);
//从某个位置开始删除到数组的尾部，并且添加0,-1,-2
var arr1=arr.splice(1,0,0);
//在第一位插入一个元素0，不删除，返回空数组
```

​		splice重构

```
function splice(arr, start, length) {
    if (start === undefined) start = 0;
    if (length === undefined) length = 0;
    start = Number(start);
    length = Number(length);
    var argumentsNum = arguments.length - 3;
    var delArr = [];
    //如果start为负数
    if (start < 0) start = arr.length + start;
    //如果length为复数
    if (length < 0) length = 0;
    //如果start大于数组长度，则向尾部插入
    if (arr.length <= start) {
        for (var i = 3; i < arguments.length; i++) {
            arr[arr.length] = arguments[i];
        }
    }
    //将从start开始length长度的元素赋值给delarr，并将arr元素前移
    for (i = 0; i < arr.length - start; i++) {
        if (i < length) {
            delArr[i] = arr[i + start];
        }
        arr[i + start] = arr[i + start + length];
    }
    //删除多余的长度
    arr.length -= length;
    //如果存在插入的参数
    if (argumentsNum >= 0) {
        arr.length += argumentsNum;
        //循环后移
        for (j = arr.length - 1; j >= start; j--) {
            arr[j] = arr[j - argumentsNum];
        }
        console.log(arr);
        //插入参数
        for (k = 0; k < argumentsNum; k++) {
            arr[k + start] = arguments[k + 3];
        }
    }
    return delArr;
}
```

##### reverse()

格式：数组.reverse()

功能：当前数组按照倒装顺序将原数组颠倒，并且返回原数组

```
var arr=[2,3,4,,6];
var arr1=arr.reverse();
console.log(arr,arr1,arr==arr1);//[2,3,4,5]	
```

​		reverse重构

```
function reverse(arr){
    var len=parseInt(arr.length/2); //二分法，然后第一个和最后一个调换
    for(var i=0;i<len;i++){
        var temp=arr[i];
        arr[i]=arr[arr.length-i-1];
        arr[arr.length-i-1]=temp;
    }
    return arr;
}
//有空元素的时候，无法赋值，直接成为undefined

或者

//定义空数组实现
function reverse(arr){
    var arr1=[];
    for(var i=0;i<arr.length;i++){
        if(i in arr){
           arr1[i]=arr[i];
        }
    }
    arr.length=0;
    for(var j=arr1.length-1;j>=0;j--){
         if(j in arr1){
           arr[arr1.length-j-1]=arr1[j];
        }
    }
    return arr;
 }

var arr1= reverse(arr);
console.log(arr1); 
arr.reverse();
console.log(arr); 
```



##### sort()

格式：数组.sort() 

功能：默认从小到大排序，按照字符串排序。

参数：一个函数，代表要怎么去进行排序（固定用法）

```
var arr = [3, 7, 2, 9, 1, 0, 6, 5, 4, 4, 12, 11];
var arr1=arr.sort();
console.log(arr,arr1,arr==arr1);
```

```
按数值大小排序
从小到大：
arr.sort(function(value1, value2){
   return value1 - value2;
   或
   return value1 > value2;
}
从大到小：
arr.sort(function(value1, value2){
   return value2 - value1;
   或
   return value2 > value1;
}
```

```
var arr=["a","c","b","d","e","ab","bc","def","aaa","efg"];
arr.sort(function(a,b){
	return a.charCodeAt(0)-b.charCodeAt(0);
});
console.log(arr);
```

​		sort重构

```
//冒泡排序
function sort(arr){
    var len=arr.length-1;
    while(len>0){
        for(var i=0;i<arr.length-1;i++){
            if(arr[i]>arr[i+1]){
                var temp=arr[i];
                arr[i]=arr[i+1];
                arr[i+1]=temp;
            }
        }
        len--;
    }
}
```

ES5新增数组方法：

##### indexOf()

格式：数组.index(item, start);

参数： item 任意的数据 	start 下标 可以不传入，默认是0

功能：在数组中查找第一次出现item元素下标，从start开始去查找

返回值： -1 没有查找到	>=0 查找到的元素的下标

```
var arr=[1,2,5,3,4,2,3,7,2,3,5]
var index=arr.indexOf(5);//下标
var index=arr.indexOf(3,4);//从第4个下标开始查找
indexOf(要搜索的元素,从第几个下标开始搜索)
console.log(index);

var index=0;
do{
    index=arr.indexOf(3,index);
    console.log(index);
}while(++index>0);
```

indexOf重构

```
function indexOf(arr,search,index){
    if(index===undefined) index=0;
    for(var i=index;i<arr.length;i++){
        if(arr[i]===search) return i;
    }
    return -1;
}
```

##### lastIndexOf()

格式：数组.index(item, start);

参数： item 任意的数据 	start 下标 可以不传入，默认是0

功能：在数组中从后向前查找第一次出现item元素下标，从start开始去查找

返回值： -1 没有查找到	>=0 查找到的元素的下标

```
var arr=[1,3,3,6,8,2,3,5,6,3,7,9,8,3,6,7,3,8,9];
var index=arr.lastIndexOf(3);
console.log(index);
```

​		lastIndexOf重构

```
function lastIndexOf(arr,search,index){
    if(index===undefined) index=0;
    for(var i=index;i>0;i--){
        if(arr[i]===search) return i;
    }
    return -1;
}
```



##### fill() 填充

格式：数组.fill(item,start,end);

参数：item要填充的值，start从什么位置开始，end到什么位置结束

返回值：填充完的数组

[注] 只能用于有长度的数组，如果不给开始位置和结束位置，就会全部填充0

```
var arr=[1,,,7];
arr.fill(5,1,3);
console.log(arr); //[1, 5, 5, 7]

var arr=[1,2,3,4,5,6];
arr.fill(10);
console.log(arr);//[10, 10, 10, 10, 10, 10]

var arr=Array(6).fill(10);
console.log(arr);
//这种方式如果填充对象，就会造成填充同一个引用地址的对象
var arr=Array(6).fill({a:1});
arr[0].a=10;
console.log(arr);
```

数组遍历：

##### forEach() 遍历

功能：遍历数组，可以获取使用元素和下标，自动过滤空元素，空元素不遍历

[注] 1、比for in来说，不会遍历到数组的属性

​		2、比for来说，不会遍历到空元素

​		3、有缺陷，函数的this指向将会被改变

```
arr.forEach(function(item, index, arr){
	/* 
		item当前遍历到的元素
		index当前遍历到元素的下标
		arr数组本身
	*/
	document.write(item + ", " + index + ", " + arr + "<br/>");
});

arr.forEach(function(item,index,arr){
	console.log(item,index,arr);
	item=10;	//错误
	arr[index]=item+10;
});
console.log(arr);
```

​		forEach重构

```
设计模式：桥接模式
function forEach(arr,fn){
	for(var i=0;i<arr.length;i++){
		if(i in arr) fn(arr[i],i,arr);
	}
} 
var arr=[2,3,4,,7,5,8];
forEach(arr,function(item,index,arr){
	console.log(item,index,arr);
}) 

或者

function forEach(arr,fn){
	for(var i=0;i<arr.length;i++){
		if(i in arr) fn(arr[i],i,arr);
	}
} 
function fn2(item,index,arr){
	console.log(item,index,arr);
} 
```

##### map() 映射

功能：遍历数组，并且使用return返回元素，这些被返回的元素会被放在一个新数组中，新数组的长度和原数组的长度相同

```
var arr = [10, 20, 30, 40, 50];
var arr1 = arr.map(function(item, index, arr){
	//遍历要做的事情  映射关系
	return item * 1.3;
});
console.log(arr1,arr);
```

​		map重构

```
function map(arr,fn){
    var arr1=[];
    for(var i=0;i<arr.length;i++){
        if(i in arr) arr1[i]=fn(arr[i],i,arr);
    }
    return arr1;
}


var arr=[1,2,5,,3,6,8];
var arr1=map(arr,function(item){
    return item+10;
});
console.log(arr1);
```

##### some() 某些

[注] :

1、遍历数组，在数组中查找每一个元素是否有符合条件，符合返回true，不符合返回false。

2、短路操作：只要找到不符合条件的元素，后面的循环就停止了。

```
var arr = [10, 20, 30, 40, 50];
var res = arr.some(function(item, index, arr){
	alert(item);
	//过滤的条件
	return item > 20;
});
```

​		some重构

```
function some(arr,fn){
    for(var i=0;i<arr.length;i++){
        if(i in arr && fn(arr[i],i,arr)) 	return true; 
    }
    return false;
}

var bool=arr.some(function(item,index,arr){
    return item>0;
})
console.log(bool)
```



##### every() 每一个

[注] :

1、遍历数组，在数组中查找每一个元素是否有符合条件，符合返回true，不符合返回false。

2、短路操作：只要找到不符合条件的元素，后面的循环就停止了。

```
var arr = [10, 20, 30, 40, 50];
var res = arr.every(function(item, index, arr){
	alert(item);
	//过滤的条件
	return item < 100;
});
```

​		every重构

```
function erery(arr,fn){
    for(var i=0;i<arr.length;i++){
        if(i in arr && !fn(arr[i],i,arr)) return false; 
    }
    return true;
} 

var bool=arr.some(function(item,index,arr){
    return item>0;
})
console.log(bool)
```

##### filter() 过滤

功能：创建一个新数组, 其包含通过所提供函数实现的测试的所有元素

[注] :如果数组中元素是对象的话，新数组和原数组有引用关系

```
var arr = [10, 20, 30, 40, 50];
筛选	筛选就是将满足条件的元素放在一个新数组中，并且返回这个新数组
var newArr = arr.filter(function(item, index, arr){
			  //过滤的条件
		return item > 20;
});
```

​		filter重构

```
function filter(arr,fn){
	var arr1 = [];
	if(arr.length===0) return [];
	
}
```

##### reduce() 归并

```
var arr = [10, 20, 30, 40, 50];
var res = arr.reduce(function(prev, next, index, arr){
	/* 
		prev 第一次是 下标为0的元素
			第二次开始 上一次遍历return的值
		next 从下标1开始，当前遍历到的元素
		index next的下标
		arr数组本身
	*/
	alert(prev + ", " + next);
	return prev + next;	//就是将prev + next重新赋给prev
});
```

​		求最大值

```
var arr = [10, 20, 30, 40, 50];
var max=arr.reduce(function(value,item){
    return value>item ? value : item; 
})
console.log(sum);
```

​		求最大值和最小值

```
var arr=[1,2,3,40,5,6,7];
var obj=arr.reduce(function(value,item){
    if(value.max==undefined) value.max=item;
    if(value.min==undefined) value.min=item;
    if(value.max<item) value.max=item;
    if(value.min>item) value.min=item;
    return value;
},{});
console.log(obj);
```

​		索引查找对象

```
var arr=[
    {id:1001,site:"网易",url:"http://www.163.com"},
    {id:1002,site:"腾讯",url:"http://www.qq.com"},
    {id:1003,site:"京东",url:"http://www.jd.com"},
    {id:1004,site:"淘宝",url:"http://www.taobao.com"},
    {id:1005,site:"天猫",url:"http://www.tmail.com"}
]

var obj=arr.reduce(function(value,item){
if(item.site==="京东") value=item;
return value;
},null);
console.log(obj);
```

- 当使用reduce设置最后的初始值时，value将会在开始为这个初始值，并且遍历将会从数组的第0项开始，item就是下标为0的元素开始

```
var arr=[1,2,3,4,5,6,7];
var sum=arr.reduce(function(value,item,index){
    console.log(value,item,index);
    return value+item;
},100);
```

​		reduce重构

```
function reduce(arr,fn,initValue){
    var index=0;
    if(initValue===undefined){
        initValue=arr[0];
        index=1;
    }
    for(;index<arr.length;index++){
        initValue=fn(initValue,arr[index],index,arr);
    }
    return initValue;
}
var sum=reduce(arr,function(value,item,index)
 
 
 
```

[注]：

- 原数组改变的方法有：push、pop、shift、unshift、splice、reverse、sort、fill

- 原数组不改变的方法有：concat、join、slice、map、filter、forEach、some、every等

- 静态方法 static

  ```
  Array.from();
  Array.isArray();
  ```

   实例方法

  ```
  arr.filter();
  arr.push();
  ```

##### 应用

​		去重

```
var arr=[1,3,3,6,8,2,3,5,6,3,7,9,8,3,6,7,3,8,9];
var len=arr.length;
for(var i=0;i<len;){
    if(arr[i]===3) arr.splice(i,1);
    else i++;
}
console.log(arr);

或者

var arr=[1,3,3,6,8,2,3,5,6,3,7,9,8,3,6,7,3,8,9];
var arr1=[];
for(var i=0;i<arr.length;i++){
    var bool=false;
    for(var j=0;j<arr1.length;j++){
        if(arr[i]===arr1[j]){
            bool=true;
            break;
        }
    }
    if(!bool) arr1.push(arr[i]);
}
arr.length=0;
for(var k=0;k<arr1.length;k++){
   arr[k]=arr1[k];
}
arr1.length=0;
arr1=null;
console.log(arr);

或者

var arr=[1,3,3,6,8,2,3,5,6,3,7,9,8,3,6,7,3,8,9];
var arr1=[];
for(var i=0;i<arr.length;i++){
    if(arr1.indexOf(arr[i])<0) arr1.push(arr[i]);
}
console.log(arr1); 

或者

var arr=[1,3,3,6,8,2,3,5,6,3,7,9,8,3,6,7,3,8,9];
for(var i=0;i<arr.length;i++){
    var index=i;
    while(index>-1){
        index=arr.indexOf(arr[i],index+1);
        if(index>-1)delete arr[i];//使用delete会变成松散型数组
    }
}
// var arr1=arr.map(function(item){
//     return item;
// });
var arr1=[];
arr.forEach(function(item){
    arr1.push(item);
})
console.log(arr1);
```

​		对象型数组某个属性排序

```
var arr=[
{id:1001,name:"苹果IphoneX",price:6900,num:2,info:"最新的苹果手机"},
{id:1002,name:"小米10",price:3900,num:3,info:"最新的小米手机"},
{id:1003,name:"华为meta10",price:8900,num:4,info:"最新的华为手机"},
{id:1004,name:"锤子手机",price:1900,num:1,info:"最新的锤子手机"},
{id:1005,name:"三星手机",price:4900,num:2,info:"最新的三星手机"},
{id:1006,name:"vivo手机",price:2900,num:4,info:"最新的vivo手机"},
{id:1007,name:"魅族手机",price:1900,num:5,info:"最新的魅族手机"},
];

arr.sort(function(a,b){
	return a.price-b.price;
})
console.log(arr);
```

​		打印超链接

```
var arr=[
    {site:"网易",url:"http://www.163.com"},
    {site:"腾讯",url:"http://www.qq.com"},
    {site:"京东",url:"http://www.jd.com"},
    {site:"淘宝",url:"http://www.taobao.com"},
    {site:"天猫",url:"http://www.tmail.com"}
]

var str="";
arr.forEach(function(item){
str+="<a href='"+item.url+"'>"+item.site+"</a><br>";
})

document.body.innerHTML+=str; 
```

​		数组排序

```
function sort(arr,fn){
    var len=arr.length-1;
    while(len>0){
        for(var i=0;i<arr.length-1;i++){
            // if(arr[i]>arr[i+1])
            // if(arr[i]-arr[i+1]>0)
            // if(a-b)
            if(fn(arr[i],arr[i+1])>0){
                var temp=arr[i];
                arr[i]=arr[i+1];
                arr[i+1]=temp;
            }
        }
        len--;
    }
}
var arr = [3, 7, 2, 9, 1, 0, 6, 5, 4, 4, 12, 11];
sort(arr,function(a,b){
    return b-a;
});
console.log(arr); 
```

​		实现imput控件点击全选

```
var all,list;
init();
function init(){
    list=document.getElementsByTagName("input");
    list=Array.from(list);
    all=list.splice(0,1)[0];
    all.onclick=clickHandler;
    list.forEach(function(item){
        item.onclick=clickHandler;
    })
}

function clickHandler(){
    //console.log(this);
    //在点击事件中this是被点击的元素
    if(this===all){
        list.forEach(function(item){
            item.checked=all.checked;
        })
    }else{
        all.checked=list.every(function(item){
            return item.checked;
        })
    }
} 
```

​		随机乱序

```
var arr=[1,2,3,4,5,6,7,8];
arr.sort(function(a,b){
    // 随机生成0-1直接的浮点数，不包括1
    return Math.random()-0.5
});
console.log(arr);
```

​		验证码

```
function getSecurityCode() {
var arr = [];
var i = 47;
while (i++ < 122) {
  if (i > 57 && i < 65) continue;
  if (i > 90 && i < 97) continue;
  arr.push(String.fromCharCode(i));
}
arr.sort(function(){
    return Math.random()-0.5;
});
arr.length=4;
return arr.join("");
}

console.log(getSecurityCode()); 
```

​		索引查找对象问题

```
var arr=[
    {id:1001,site:"网易",url:"http://www.163.com"},
    {id:1002,site:"腾讯",url:"http://www.qq.com"},
    {id:1003,site:"京东",url:"http://www.jd.com"},
    {id:1004,site:"淘宝",url:"http://www.taobao.com"},
    {id:1005,site:"天猫",url:"http://www.tmail.com"}
] 

var index=arr.indexOf({id:1001,site:"京东",url:"http://www.jd.com"});


function searchObj(arr,obj){
for(var i=0;i<arr.length;i++){
  if(arr[i].id===obj.id) return i;
}
return -1;
} 

或者

var arr=[
    {site:"网易",url:"http://www.163.com"},
    {site:"腾讯",url:"http://www.qq.com"},
    {site:"京东",url:"http://www.jd.com"},
    {site:"淘宝",url:"http://www.taobao.com"},
    {site:"天猫",url:"http://www.tmail.com"}
]
function searchObj(arr,obj){
    for(var i=0;i<arr.length;i++){
        if(JSON.stringify(arr[i])===JSON.stringify(obj)) return i;
    }
    return -1;
}

var index=searchObj(arr,{site:"京东",url:"http://www.jd.com"});
console.log(index);
```

#### 二维数组

```
var arr=[[1,2,3],[4,5,6],[7,8,9]];
arr[0][1]
```

无论二维数组还是对象型数组，都是有引用关系的

```
var arr=[];
for(var i=0;i<10;i++){
    arr[i]=[];
    for(var j=0;j<10;j++){
        arr[i][j]=i*10+j;
    }
}
console.log(arr);

var arr=[
    {a:1,b:2},
    {a:1,b:2},
    {a:1,b:2},
    {a:1,b:2}
]
```

扁平化数组

```
var arr=[[1,2,3],[4,5,6,2],[7,5,8,9]];
var arr1=arr.flatMap(function(item,index,arr){
    console.log(item);
    return item;
});
console.log(arr1);
```

​		扁平化数组重构

```
function flatMap(arr,fn){
    var arr1=[];
    for(var i=0;i<arr.length;i++){
        if(Array.isArray(fn(arr[i],i,arr))){
            for(j=0;j<arr[i].length;j++){
                arr1.push(arr[i][j]);
            }
        }else{
            arr1.push(arr[i]);
        }
    }
    return arr1;
}

var arr=[0,"我",[1,2,3],[4,5,6],[7,8,9]];
var arr1=flatMap(arr,function(item,index,arr){
    return item;//返回数组中的数组
})
console.log(arr1);
```



#### 排序

##### 冒泡排序

- 规则：前后两个数两两进行比较，如果符合交换条件就交换两个数位置。
- 规律：冒泡排序每一轮排序，都可以找出一个较大的数，放在正确的位置。

```
9, 8, 7, 6, 5, 4
第一轮：五次
	9, 8, 7, 6, 5, 4
	8, 9, 7, 6, 5, 4
	8, 7, 9, 6, 5, 4
	8, 7, 6, 9, 5, 4
	8, 7, 6, 5, 9, 4
	8, 7, 6, 5, 4, 9

第二轮：四次
	8, 7, 6, 5, 4
	7, 8, 6, 5, 4
	7, 6, 8, 5, 4
	7, 6, 5, 8, 4
	7, 6, 5, 4, 8

第三轮：三次
	7, 6, 5, 4
	6, 7, 5, 4
	6, 5, 7, 4
	6, 5, 4, 7
                
第四轮：两次
    6, 5, 4
    5, 6, 4
    5, 4, 6
                
第五轮：一次
    5, 4
    4, 5
    
分析：
    比较轮数 = 数组长度 - 1;
    每一轮比较的次数 = 数组长度 - 当前的轮数。
    
function sort(arr){
    var len=arr.length-1;
    while(len>0){
        for(var i=0;i<arr.length-1;i++){
            if(arr[i]>arr[i+1]){
                var temp=arr[i];
                arr[i]=arr[i+1];
                arr[i+1]=temp;
            }
        }
        len--;
    }
}
```

##### 选择排序

- 规则：选出一个位置，这个位置上的数，和后面所有的数进行比较，如果比较出大小就交换两个数位置。
- 规律：每一轮都能选出一个最小的数，放在正确的位置。

```
第一轮：五次
    9, 8, 7, 6, 5, 4
    8, 9, 7, 6, 5, 4
    7, 9, 8, 6, 5, 4
    6, 9, 8, 7, 5, 4
    5, 9, 8, 7, 6, 4
    4, 9, 8, 7, 6, 5

第二轮：四次
       9, 8, 7, 6, 5
       8, 9, 7, 6, 5
       7, 9, 8, 6, 5
       6, 9, 8, 7, 5
       5, 9, 8, 7, 6

第三轮：三次
          9, 8, 7, 6
          8, 9, 7, 6
          7, 9, 8, 6
          6, 9, 8, 7

第四轮：两次
	         8, 9, 7
             7, 9, 8
    
第五轮：一次
                9, 8
    			8, 9

比较的轮数 = 数组长度 - 1;
每一轮比较的次数 = 数组长度 - 当前的轮数


var arr=[2,7,1,4,6];
min 0      7 2  arr[0]
min 0      1 2   arr[0]
min 2      4 1   arr[2]
min 2      6 1   arr[2]
min 2    
用当前项和最小项交换    
1,7,2,4,6

1,7,2,4,6
min 1      2 7  arr[1];
min 2      2 4  arr[2];
min 2      2 6   arr[2];
min  2     
用当前项和最小项交换    
1,2,7,4,6

1,2,7,4,6
min 2    7 4  arr[2]
min 3    4 6  arr[3]
min 3    
用当前项和最小项交换    
1,2,4,7,6

1,2,4,7,6
min 3    7 6  arr[3]
min 4    6 7
min 4 
用当前项和最小项交换 
1,2,4,6,7

function selectionSort(arr) {
        var len = arr.length;
        var minIndex, temp;
        for (var i = 0; i < len - 1; i++) {
          minIndex = i;
          for (var j = i + 1; j < len; j++) {
            if (arr[j] < arr[minIndex]) {
              minIndex = j; //将最小数的索引保存
            }
          }
          temp = arr[i];
          arr[i] = arr[minIndex];
          arr[minIndex] = temp;
        }
        return arr;
      }
```

##### 快速排序

- 规则：从数组中选定一个基数（中间数），然后把数组中的每一项与此基数做比较，小的放入一个新数组，大的放入另外一个新数组。然后再采用这样的方法操作新数组。直到所有子集只剩下一个元素，排序完成。

```
1,5,2,7,3
中2    [1,5,7,3]
left [1]   right [5,7,3]; 
5,7,3   
中7   left 5,3
中3  right 5  
3,5    中+右  
3,5,7  上面的值+ 中 
1,2,3,5,7   [1].concat(2)+[3,5,7]  左+中+上面的值


function quickSort(arr) {
	if (arr.length <= 1) {
		return arr;
    }
    var pivotIndex = parseInt(arr.length / 2);
    var pivot = arr.splice(pivotIndex, 1)[0];
    var left = [];
    var right = [];
    for (var i = 0; i < arr.length; i++) {
      if (arr[i] < pivot) {
        left.push(arr[i]);
      } else {
        right.push(arr[i]);
      }
    }
    return quickSort(left).concat([pivot], quickSort(right));
} 
var arr1 = quickSort(arr);
console.log(arr1);
```

