## 内建对象

#### Math

##### Math的属性

[注] 常量数据不能修改

E	返回算术常量 e，即自然对数的底数（约等于2.718）。
LN2	返回 2 的自然对数（约等于0.693）。
LN10	返回 10 的自然对数（约等于2.302）。
LOG2E	返回以 2 为底的 e 的对数（约等于 1.414）。
LOG10E	返回以 10 为底的 e 的对数（约等于0.434）。
PI	返回圆周率（约等于3.14159）。
SQRT1_2	返回返回 2 的平方根的倒数（约等于 0.707）。
SQRT2	返回 2 的平方根（约等于 1.414）。



##### Math的方法

abs(x)	返回数的绝对值。
acos(x)	返回数的反余弦值。
asin(x)	返回数的反正弦值。
atan(x)	以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。
atan2(y,x)	返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。
ceil(x)	对数进行上舍入。
cos(x)	返回数的余弦。
exp(x)	返回 e 的指数。
floor(x)	对数进行下舍入。
log(x)	返回数的自然对数（底为e）。
max(x,y)	返回 x 和 y 中的最高值。
min(x,y)	返回 x 和 y 中的最低值。
pow(x,y)	返回 x 的 y 次幂。
random()	返回 0 ~ 1 之间的随机数。
round(x)	把数四舍五入为最接近的整数。
sin(x)	返回数的正弦。
sqrt(x)	返回数的平方根。
tan(x)	返回角的正切。

abs  绝对值  非负值

```
console.log(Math.abs(-5.352));
```

将小数点求整数

Math.ceil(); 向上舍入

```
var a=3.2;
console.log(Math.ceil(a));//整数+1	4
```

Math.floor(); 向下舍入

```
var a=3.2;
console.log(Math.floor(a));//3
```

Math.round(); 四舍五入

```
var a=3.54;
console.log(Math.round(a));

var a=-3.4    
//-3.6    -4+0.4=-4 
//-3.5   -4+0.5=-4+1=-3
console.log(Math.round(a));
```

max  min

```
var max=Math.max(3,5,7);
console.log(max);

var min=Math(1,5,8);
```

​		求数组的最大值和最小值（背）

```
var arr=[2,24,5,7,3,2,1,7,4,22,56];
var max=Math.max.apply(null,arr);
var min=Math.min.apply(null,arr);
console.log(max,min);
```

sqrt 平方根  	pow 幂

```
var n=Math.sqrt(4);
console.log(n);
```

```
var a=10;
var s=Math.pow(a,2);//多少次幂
var s=Math.pow(a,1/2);//开平方根，但是跟sqrt比效率低
```

random

​		从最小值到最大值

```
Math.random()   //0-1

function random(min,max){
	return Math.random()*(max-min)+min;
}
console.log(random(10,20));
```

#### Number

##### Number的属性

MAX_VALUE	可表示的最大的数。（正数的）
MIN_VALUE	可表示的最小的数。
NaN	非数字值。（Number.NaN）
NEGATIVE_INFINITY	负无穷大，溢出时返回该值。
POSITIVE_INFINITY	正无穷大，溢出时返回该值。

##### Number的方法

toString	把数字转换为字符串，使用指定的基数。
toLocaleString	把数字转换为字符串，使用本地数字格式顺序。
toFixed	把数字转换为字符串，结果的小数点后有指定位数的数字。
toExponential	把对象的值转换为指数计数法。
toPrecision	把数字格式化为指定的长度。

toLocaleString	把数字转换为字符串，使用本地数字格式顺序。

```
var a=10;
a= a.toLocaleString();
console.log(a);
```

toExponential	把对象的值转换为指数计数法。

```
var a=356.274;
console.log(a.toPrecision(2));//1-21   四舍五入的作用
```

toPrecision	把数字格式化为指定的长度。

```
var a=356.274;
console.log(a.toExponential(2));//0-20	小数点后的长度
```

#### String基础

```
var  str="aa";	//栈中
var str1=new String("aa");	//堆中
```

##### length 

字符长度 只读（只能获取，不能修改）

```
var str="aaaa";
str.length=0;//ES6 报错
console.log(str.length);
```

##### 查找字符串元素

```
var str="abcd";
console.log(str[1]);//b
str[1]="e";  禁止使用这种方式修改字符串

console.log(str.charAt(1));	//str[1],查找字符串中下标为几的元素

console.log(str.indexOf("a"));//查找a字符是否在字符串中存在，如果不存在返回-1
str.indexOf("a",position);//position起始位置

str.lastIndexOf("a")  从尾部向前查找
```

​		模糊查找

```
var arr=[
    {id:1001,name:"计算机",price:4999},
    {id:1002,name:"电机",price:1999},
    {id:1003,name:"记事本",price:9},
    {id:1004,name:"课本",price:99},
    {id:1005,name:"计算器",price:149},
];

var arr1=arr.filter(function(item){
	return item.name.indexOf("计")>-1;
})
console.log(arr1);
```

​		表格案例（数据驱动显示）

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

var table;
init();
function init(){
    document.write("<table id='table'></table>");
    table=document.getElementById("table");
    search=document.getElementById("search");
    createTable(arr);
    search.oninput=inputHandler;
}

function createTable(arr){
    var str="";
    for(var i=0;i<arr.length;i++){
        if(i===0){
            str+="<tr>";
            for(var prop in arr[0]){
                str+="<th>"+prop+"</th>";
            }
            str+="</tr>";
        }
        str+="<tr>";
        for(var p in arr[i]){
            str+="<td>"+arr[i][p]+"</td>";
        }
        str+="</tr>";
    }
    table.innerHTML=str;
}

function inputHandler(){
    // search.value input输入的内容
    var arr1=arr.filter(function(item){
        return item.name.indexOf(search.value)>-1;
    })
    createTable(arr1);
}
```



##### 字符串连接

```
console.log(str.concat("eeee"));	//str+="eeee";

var age=10;
console.log("今年你"+age+"岁了");
console.log("今年你".concat(age,"岁了"))
```

##### 其他方法

charCodeAt	fromCharCode

```
console.log(str.charCodeAt(0));//获取下标是0的字符的Unicode编码
String.fromCharCode(97); //编码转换为字符串
```

replace

```
var str="abcdef";
str=str.replace("b","z");//字符串的方法不能修改原字符，返回替换后的新字符串，暂时只能替换一个字符
str=str.replace("c","c1");//既是替换又是插入字符
str=str.replace("cd",function(item){
	console.log(item);
	return item+"1";
})
console.log(str); //abcd1ef
```

search

```
var str="abcde";
var index=str.search("a");
//search可以用于正则表达式查找
```

match
字符串的正则表达式，将查找的结果以数组的形式返回

```
var arr=str.match("c")
console.log(arr);
```

slice

和数组的slice等同

```
function randomColor(){
    var col="#";
    for(var i=0;i<6;i++){
        col+=Math.floor(Math.random()*16).toString(16);
    }
    return col;
} 

或者

function randomColor(){
    var col="rgb(";
    for(var i=0;i<3;i++){
        col+=Math.floor(Math.random()*256)+","
    }
    col=col.slice(0,-1)+")";
    return col;
}

或者
function randomColor(){
	return "#"+Array(6).fill(Math.floor(Math.random()*16).toString(16)).join("");
}

var div0=document.getElementById("div0");
div0.style.backgroundColor=randomColor();
div0.onclick=function(){
    div0.style.backgroundColor=randomColor();
}
```

substring

格式：str.substring(start,end);	截取字符串从start到end结束 [start,end)

1、substring，start和end都不支持负数，负数代表0之前，就是最前面

2、slice只能从前向后选，substring可以从后向前选

```
var str="abcdefg";
console.log(str.substring(5,2));

var str="中国的四大名著中《西游记》是吴承恩写的"; //取出西游记三个字
str=str.substring(str.indexOf("《")+1,str.indexOf("》"));
console.log(str);
```

substr

格式：str.substr(start,length);

截取从字符串start开始，按照给出长度截取固定的字符串

```
var str="中国的四大名著中《西游记》是吴承恩写的";
str=str.substr(str.indexOf("《")+1,3);
console.log(str);
```

toUpperCase 转成大写

```
console.log(str.toUpperCase());
```

toLowerCase转成小写

```
console.log("XIETIAN".toLowerCase());
```

split	切割，使用某个符号切割并把切割的元素转为数组，和数组的join相反

```
var arr=[1,2,3,4,5,6];
var str=arr.join("#");
var arr1=str.split("#");
console.log(arr1);

var str="abcdef";
var arr=str.split("");
console.log(arr);

转换成数组，然后反转，再用""连接
var str="abcdef";
str=str.split("").reverse().join("");
console.log(arr);

var url="https://detail.tmall.com/item.htm?id=570063940353&ali_refid=a3_430406_1007:116401153:J:157145175_0_1069023083:ddc80320c499f96850f409bbea969fa6&ali_trackid=85_ddc80320c499f96850f409bbea969fa6&spm=a21bo.2017.201874-sales.15";
url=url.split("?").shift().join("");
或者
url=url.split("?")[1];
function getURLPram(url){
    url=url.split("?")[1];
    var obj={};
    var arr=url.split("&");
    for(var i=0;i<arr.length;i++){
        var str=arr[i];
       var arr1=str.split("=");
        obj[arr1[0]]=arr1[1];
    }
    return obj;
}
或者
function getURLPram(url){
    return url.split("?")[1].split("&").reduce(function(value,item){
         var arr=item.split("=");
         value[arr[0]]=arr[1];
         return value;
    },{})
 }
```

#### Date

##### 获取时间对象

```
var date=new Date();
console.log(date);
```

##### 时间的获取方法

Date()	返回当日的日期和时间。
getDate()	从 Date 对象返回一个月中的某一天 (1 ~ 31)。

```
var day=date.getDate();//日期
```

getDay()	从 Date 对象返回一周中的某一天 (0 ~ 6)。

```
var week=date.getDay();//星期  0-6  0星期日
```

getMonth()	从 Date 对象返回月份 (0 ~ 11)。

```
var month=date.getMonth();//0-11
```

getFullYear()	从 Date 对象以四位数字返回年份。

```
var year=date.getFullYear();
```

getYear()	请使用 getFullYear() 方法代替。
getHours()	返回 Date 对象的小时 (0 ~ 23)。
getMinutes()	返回 Date 对象的分钟 (0 ~ 59)。
getSeconds()	返回 Date 对象的秒数 (0 ~ 59)。
getMilliseconds()	返回 Date 对象的毫秒(0 ~ 999)。
getTime()	返回 1970 年 1 月 1 日至今的毫秒数。

时间戳，永远不重复
var time=date.getTime();

```
//效率高
function fn1(){
    var s=0;
    for(var i=0;i<1000;i++){
        s+=i;
    }
}

//效率低
function fn2(s,i){
    if(!s) s=0;
    if(!i) i=0;
    i++;
    s+=i;
    if(i<1000) fn2(s,i); 
}

测试时间运行效率（一）
var time=new Date().getTime();
for(var i=0;i<10000;i++){
    fn1();
}
console.log(new Date().getTime()-time);
time=new Date().getTime();
for(var j=0;j<10000;j++){
    fn2();
}
console.log(new Date().getTime()-time);

测试时间运行效率（二）
封装
var Utils=(function(){
    var time=0;
    var ids=0;
    var timeManage={};
    return {
        timeStart:function(){
            if(time) return;
            time=new Date().getTime();
        },
        timeEnd:function(){
            var t=new Date().getTime()-time;
            time=0;
            return t;
        },
        ts:function(){
            ids++;
            timeManage[ids]=new Date().getTime();
            return ids;
        },
        te:function(id){
            if(!timeManage[id]) return 0;
            var t=new Date().getTime()-timeManage[id];
            delete timeManage[id];
            return t;
        },
        randomColor:function(){
            var col="#";
            for(var i=0;i<6;i++){
                col+=Math.floor(Math.random()*16).toString(16);
            }
            return col;
        }
    }
})();

Utils.timeStart();
for(var j=0;j<10000;j++){
    fn1();
}
console.log(Utils.timeEnd());
Utils.timeStart();
for(var j=0;j<10000;j++){
    fn2();
}
console.log(Utils.timeEnd());

测试时间运行效率（三）	推荐
var id1=Utils.ts()
for(var j=0;j<10000;j++){
    fn1();
}
var id2=Utils.ts();
for(var j=0;j<10000;j++){
    fn2();
}
console.log(Utils.te(id2));
console.log(Utils.te(id1));
```

getUTCHours()	返回格林尼治时间

```
var h=date.getUTCHours();
```

toLocaleString	转换为本地时间

```
console.log(date.toLocaleString());
```

toUTCString()	转换为格林尼治时间，后面的cookie使用

```
console.log(date.toUTCString());
```



##### 时间的设置方法

[注] 任何设置如果数值大于该值域的最大值时，就会进位

setDate()	设置 Date 对象中月的某一天 (1 ~ 31)。
setMonth()	设置 Date 对象中月份 (0 ~ 11)。

```
date.setMonth(12); //一月
```

setFullYear()	设置 Date 对象中的年份（四位数字）。

```
date.setFullYear(2021);
```

setYear()	请使用 setFullYear() 方法代替。
setHours()	设置 Date 对象中的小时 (0 ~ 23)。
setMinutes()	设置 Date 对象中的分钟 (0 ~ 59)。

```
date.setMinutes(date.getMinutes()+30);//设置30分钟后
```

setSeconds()	设置 Date 对象中的秒钟 (0 ~ 59)。
setMilliseconds()	设置 Date 对象中的毫秒 (0 ~ 999)。
setTime()	以毫秒设置 Date 对象。

应用：

每次new Date就会获取new这个时间的当时值

```
var date=new Date();
console.log(date.getSeconds());

setTimeout(function(){
    var d=new Date();
    console.log(d.getSeconds());
},2000)
```

秒表

```
<style>
    #timeCon
    {
        font-size: 25px;
        font-weight: 700;
    }
</style>

<body>
    <div id="timeCon">00:00:00</div>
    <button id="startBn">启动</button>&emsp;<button id="resetBn">复位</button>
    <script>
        var startBn,
            timeCon,
            resetBn,
            temptime=0,
            startTime=0,
            bool=true;
        init();
        function init(){
            startBn=document.getElementById("startBn");
            timeCon=document.getElementById("timeCon");
            resetBn=document.getElementById("resetBn");
            startBn.onclick=clickHandler;
            resetBn.onclick=resetClickHandler;
            setInterval(animation,16);
        }

        function clickHandler(){
            bool=!bool;
            if(bool){
                startBn.innerHTML="启动"
                temptime+=new Date().getTime()-startTime;
                startTime=0;
            }else{
                startBn.innerHTML="暂停"
                startTime=new Date().getTime();
            }
        }

        function resetClickHandler(){
            bool=true;
            temptime=0;
            startTime=0;
            timeCon.innerHTML="00:00:00";
            startBn.innerHTML="启动"
        }


        function animation(){
            if(bool) return;
            var time=new Date().getTime();
            var s=Math.floor((time-startTime+temptime)/1000);
            var m=Math.floor(s/60);
            s=s%60;
             var ms=Math.floor((time-startTime+temptime)%1000/10);
             timeCon.innerHTML=(m<10 ? "0"+m : m)+":"+(s<10 ? "0"+s : s)+":"+(ms<10 ? "0"+ms : ms)
        }
    </script>
</body>
```

