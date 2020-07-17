## BOM

- window-->BOM		Browser Object Model 

  document-->DOM		Document Object Model

- BOM和BOM都有Object对象，所以有属性和方法

- ​                                              window

  location 本地 	history 历史	screen 屏幕	navigator 信息

#### window对象

open()

因为浏览器自带屏蔽窗口，所以现在不用了

```
document.onmousemove=function(){
	open("http://www.163.com","网易","width=400,height=400");
}
```

close()

```
document.onmousemove=function(){
	close("http://www.163.com","网易","width=400,height=400");
}
```

innerHeight 	innerWidth

浏览器窗口的内部宽度(兼容所有浏览器)
浏览器窗口的内部高度(兼容所有浏览器)—包含滚动条

```
console.log(innerWidth,innerHeight);	
```

outerWidth 	outerHeight

可以获取浏览器窗口的整个宽
可以获取浏览器窗口的整个高

```
console.log(outerWidth,outerHeight);
```

screenLeft 	screenTop 

窗口距离屏幕左上角的位置

```
console.log(screenLeft,screenTop)
```

screenX 	screenY 

窗口距离屏幕左上角的位置

```
console.log(screenX,screenY)
```

#### location对象

reload()

​	重新加载当前页面

```
 location.reload();//重载，刷新当前页面
```

href 

```
location.href="http://www.163.com";
console.log(location.href) //获取当前页面地址
```

assign()

```
location.assign("http://www.163.com");
```

replace()

```
location.replace("http://www.163.com");
```

【注】：1、href 、assign()有历史记录，可以回退，replace()没有历史记录

​				2、assign()、replace()是方法，href是属性（可以设置，还可以获取）

hash

```
console.log(location.hash);//获取#号后面的锚点
```

search

```
console.log(location.search);//获取?号后面的参数
```

hostname 
	返回 web 主机的域名

```
console.log(location.hostname);
```

pathname 
	返回当前页面的路径和文件名

```
console.log(location.pathname);
```

port 
	返回 web 主机的端口 （80 或 443）

```
console.log(location.port);
```

protocol 
	返回所使用的 web 协议（http:// 或 https://）

```
console.log(location.protocol);
```

#### history对象

​	回退和前进的地址

back()

```
history.back(); //回退
```

forward()

```
history.forward();	//前进
```

go()

```
history.go(-1);//回退1
history.go(0);//刷新
history.go(1);//前进1
```

pushState()

```
history.pushState({a:1},"shop","?data="+n);	
//在history栈中添加一个新的条目，发生跳转了
```

replaceState()

```
history.replaceState({a:1},"aa");
//替换当前的记录值，没有发生跳转
```



#### screen对象

availHeight	availWidth

​	屏幕的高度像素减去系统部件高度之后的值

​	屏幕的宽度像素减去系统部件宽度后的值

（不包含任务栏宽高）

```
console.log(screen.availWidth,screen.availHeight);
```

height	width

​	屏幕的高度像素

​	屏幕的宽度像素

（包含任务栏宽高）

```
console.log(screen.width,screen.height);
```

#### navigator对象

userAgent
	返回由客户机发送服务器的 user-agent 头部的值

```
console.log(navigator.userAgent);
```

​		根据打开的浏览器，获取浏览器信息

```
console.log(getBrowserInfo());
function getBrowserInfo(){
    if(navigator.userAgent.indexOf("Chrome")>-1) return "Chrome:"+navigator.userAgent.split("Chrome")[1].split(" ")[0].slice(1);
    if(navigator.userAgent.indexOf("Firefox")>-1) return "Firefox:"+navigator.userAgent.split("Firefox")[1].slice(1);
}
```

appName
	返回浏览器的名称。

appVersion
	返回浏览器的平台和版本信息。

platform
	返回运行浏览器的操作系统平台。

#### 应用

普通列表

```
<style>
    div{
        width: 100px;
        height: 40px;
        font-size: 30px;
        line-height: 40px;
        text-align: center;
        border:1px solid #000000;
        float: left;
        margin-left: 50px;
        user-select: none;
    }
    p{
        clear: both;
        display: none;
    }
   
</style>
</head>
<body>
<div>水果</div>
<div>蔬菜</div>
<div>零食</div>
<div>饮料</div>
<br>
<br>
<p>猕猴桃
    苹果
    梨</p>
<p>白菜
    土豆
    地瓜</p>
<p>辣条
    牛肉干
    薯片</p>
<p>可乐
    雪碧
    果汁</p>
<script>
    var arr,divs;
    init()
    function init(){
        arr=Array.from(document.getElementsByTagName("p"));
        divs=Array.from(document.getElementsByTagName("div"));
        arr[0].style.display="block";
        for(var i=0;i<divs.length;i++){
            divs[i].onclick=clickHandler;
        }
    }


    function clickHandler(){
       var index=divs.indexOf(this);
        for(var i=0;i<arr.length;i++){
            if(i===index){
                arr[i].style.display="block";
            }else{
                arr[i].style.display="none";
            }
        }
    }
</script>
```

历史列表

```
<style>
    div{
        width: 100px;
        height: 40px;
        font-size: 30px;
        line-height: 40px;
        text-align: center;
        border:1px solid #000000;
        float: left;
        margin-left: 50px;
        user-select: none;
    }
    p{
        clear: both;
        display: none;
    }
   
</style>
</head>
<body>
<div>水果</div>
<div>蔬菜</div>
<div>零食</div>
<div>饮料</div>
<br>
<br>
<p>猕猴桃
    苹果
    梨</p>
<p>白菜
    土豆
    地瓜</p>
<p>辣条
    牛肉干
    薯片</p>
<p>可乐
    雪碧
    果汁</p>
<script>
    var arr,divs;
    init()
    function init(){
        // 当历史前进或者后退时就会收到这个事件
        window.onpopstate=popStateHandler;
        arr=Array.from(document.getElementsByTagName("p"));
        divs=Array.from(document.getElementsByTagName("div"));
        arr[0].style.display="block";
        for(var i=0;i<divs.length;i++){
            divs[i].onclick=clickHandler;
        }
        
    }


    function clickHandler(){
       var index=divs.indexOf(this);
    	//history.pushState({state:1},"","#"+this.innerHTML);
        // 在历史记录列表中增加数据，后面的#内容标示当前跳转部分
         history.pushState({index:index}, "", "#" +this.innerHTML);
         changeMenu(index);
    }

    function popStateHandler(){
        console.log(history.state);
        changeMenu(history.state.index)
    }

   function changeMenu(index){
    for(var i=0;i<arr.length;i++){
            if(i===index){
                arr[i].style.display="block";
            }else{
                arr[i].style.display="none";
            }
        }
   }
</script>
```



## DOM

#### 节点

##### 节点属性

node  标签  注释  文本  文档

nodeName（节点名称） 

- ​	元素节点的 nodeName 是标签名称 

- ​	文本节点的 nodeName 永远是 #text 

- ​	注释节点的 nodeName 永远是 #comment

- ​    任何标签的nodeName都是该标签的大写字母

  ```
  console.log(document.body.firstChild.nodeName==="DIV");
  console.log(document.body.firstChild.constructor===HTMLDivElement);
  ```

nodeValue（节点值）

- ​	文本节点nodeValue 属性包含文本。

- ​	元素节点nodeValue不可用

- ​	注释节点nodeValue包括注释内容

```
console.log(document.body.firstChild.nodeValue);
```

nodeType（节点类型）

- ​	元素---1
  ​	属性----2
  ​	文本----3
  ​	注释---8
  ​	文档----9

```
console.log(document.body.firstChild.nodeType);
```

##### 获取Dom元素

​	document.getElementById()

- 通过id获取元素

```
document.getElementById("id");
```

​	document.getElementsByTagName()

- 通过标签名获取标签列表，只能通过document获取，获取的是HTMLCollection

```
document.getElementsByTagName("div");
```

​	document.getElementsByName()

- 可以在xml中使用
- 可以在form表单中获取input控件
- `<div name="sex"></div>`不能用，没有意义，可以获取，因为这是在xml中的格式
- 通过name属性获取节点列表，只能通过document获取，获取的是NodeList
- NodeList可以用forEach遍历

```
var list=document.getElementsByName("sex");
list.forEach(function(item){
	console.log(item);
})
```

​	document.getElementsByClassName()

- 通过Class名获取标签列表，任何标签都可以获取其子项中Class列表，获取的是HTMLCollection

```
var list=document.getElementsByClassName("div1");

var div0=document.getElementById("div0");
var list=div0.getElementsByClassName("div1");
```

​	document.querySelector(所有选择器)  根据选择器列表获取第一个元素

```
var div=document.querySelector("#div0");
var div=document.querySelector(".div1");
var div=document.querySelector("[type=text]");
var div=父容器.querySelector()
```

​	document.querySelectorAll(所有选择器)  获取选择器列表的中所有元素

##### 节点遍历

childNodes：所有子节点（包括注释）

```
console.log(document.body.childNodes);//所有子节点列表
```

children：获取所有子元素

```
console.log(document.body.children);//所有子元素的列表
```

parentNode：获取已知节点的父节点

```
console.log(document.body.firstChild.parentNode);
```

parentElement：获取已知元素的父元素

```
console.log(document.body.firstChild.parentNode);
```

firstElementChild : 第一个子元素

```
console.log(document.body.firstElementChild);//第一个子元素
```

firstChild : 第一个子节点

```
console.log(document.body.firstChild);
```

lastElementChild：最后一个子元素

```
console.log(document.body.lastElementChild);
```

lastChild：最后一个子节点

```
console.log(document.body.lastChild);
```

nextElementSibling：下一个兄弟元素

```
console.log(document.body.firstElementChild.nextElementSibling);
```

nextSibling：下一个兄弟节点

```
console.log(document.body.firstElementChild.nextSibling);
```

previousElementSibling：上一个兄弟元素

```
console.log(document.body.lastElementChild.previousElementSibling);
```

previousSibling：上一个兄弟节点

```
console.log(document.body.lastElementChild.previousSibling);
```

##### 创建节点

​	document.createElement("标签名") : 创建新元素

```
var div=document.createElement("div");
div.style.width="100px";
div.style.height="100px";
div.style.backgroundColor="red";
//  appendChild追加到子元素中    父元素.appendChild(子元素)
document.body.appendChild(div);

var script=document.createElement("script");
var img=document.createElement("img");
var table=document.createElement("table");
```

​		点击创建元素

```
var bn=document.querySelector("button");
bn.onclick=function(){
	var div=document.createElement("div");
	document.body.appendChild(div);
}

或者

function ce(type,style,parent){
    var elem=document.createElement(type);
    for(var prop in style){
        elem.style[prop]=style[prop];//elem.style[prop]等同于elem.style.width
    }
    if(typeof parent==="string") parent=document.querySelector(parent);
    if(parent){
        parent.appendChild(elem);
    }
    return elem;
}

var div=ce("div",{
    width:"50px",
    height:"50px",
    backgroundColor:"red"
},"#div0");
document.body.appendChild(div);

或者

document.addEventListener("click",clickHandler);

function clickHandler(e){
   Utils.ce("div",{
      width:"50px",
      height:"50px",
      backgroundColor:Utils.randomColor(),
      position:"absolute",
      left:e.x-25+"px",
      top:e.y-25+"px"
   },"body");
}
```

document.createDocumentFragment(): 碎片容器，直接插入到文档中

```
var ul=document.createElement("ul");
  for(var i=0;i<10;i++){
    var li=document.createElement("li");
    li.innerHTML=i;
    ul.appendChild(li);
}
document.body.appendChild(ul);



var con=document.createDocumentFragment();
for(var i=0;i<10;i++){
    var div=document.createElement("div");
    con.appendChild(div);
}
document.body.appendChild(con);
```

document.createTextNode("") : 创建文本节点

```
var txt=document.createTextNode("你好");
div0.insertBefore(txt,div0.firstElementChild)
```

##### 插入节点

​	appendChild(node) : 向childNodes末尾插入一个节点node

```
var div=document.createElement("div");
div.textContent="你好";//给div设置文本内容，不能设置html
document.body.appendChild(div);
```

​	insertBefore(newElement,targetElement) : 向targetNode之前插入节点node

```
父容器.insertBefore(要插入的元素,插入在谁的前面);
document.body.insertBefore(div,document.body.firstChild)
```

【注】：

```
var div0=document.querySelector("#div0");

// 插入在子元素的最尾部
   div0.appendChild(span);	//在里面的最后
// 插入在子元素的最前面
   div0.insertBefore(span,div0.firstChild);	//在里面的最前
// 插入在元素的兄弟项前面
   div0.parentElement.insertBefore(span,div0);	//在前面
// 插入在元素的兄弟项后面
   div0.parentElement.insertBefore(span,div0.nextSibling);	//在后面
```

##### 替换节点

​	replaceChild(newNode,oldNode) : newNode替换节点oldNode

```
//父容器.replaceChild(新的子元素，要替换掉旧元素);
var p=document.createElement("p")
div0.replaceChild(p,div0.firstElementChild);
```

##### 删除节点

​	removeChild(node) : 移除父节点的某个子节点

```
父容器.removeChild(子元素);
```

​	remove()：移除当前节点

```
子元素.remove()
```

【注】在删除时，元素仅仅是从页面中删除，不是从内存中删除，如果没有清除内			存的情况下还可以加入回去

```
div0.remove();
document.body.appendChild(div0);


div0.addEventListener("click",clickhandler);
function clickhandler(){
	console.log("aaa");
}
div0.remove();
div0=null;//需要在设值null之前将事件也需要删除
document.body.appendChild(div0);


//要考虑有没有加事件
div0.textContent="";
div0.innerHTML="";
```

##### 复制节点

​	cloneNode(boolean) : 复制一个标签

- ​	复制元素=复制目标.cloneNode(深浅复制)
  - true	深复制，复制元素和元素的所有子元素和节点
  - false   浅复制，仅复制当前标签

```
var span1=document.querySelector("#span1");
var span2=span1.cloneNode(false);
// 复制标签时，会标签的属性一起复制
span2.id="span2";
div0.appendChild(span2);
```

#### Dom属性

##### Dom对象属性

由于所有的DOM元素都是Object类型,所以我们可以通过对象的方式为DOM元素设置属性

- DOM的对象属性，分为自定义型和原DOM对象属性
- DOM的对象原属性与DOM对象的标签属性部分对应，部分有差别

```
div.className="div1";//就是设置class标签属性

div.aa=10;
console.log(div.aa);
```

##### Dom标签属性

直接写在标签上的属性

- 设置标签的属性和值，值和属性都必须是字符
- DOM的标签属性命名，不能使用大小写区分不适用下划线区分，属性名必须全小写字母，并且使用-区分每个单词

```
div.setAttribute("aa","10");
div.setAttribute("shop-data","10");

//获取标签属性
console.log(div.getAttribute("shop-data"));
//删除标签属性
div.removeAttribute("shop-data");
```

##### Dom常用属性

​	document.body：body元素

​	document.title：获取、设置文档的标题

​	document.URL：获得完整的URL

​	document.domain：获取域名

##### 获取节点上的属性

​	getAttribute(属性)：

##### 给节点创建一个新属性

​	setAttribute(属性,值)：

##### 删除一个节点上的属性

​	removeAttribute(name)

#### Dom对象的样式

##### 设置Dom对象的样式

​	dom.style.styleName=""（行内样式）

```
var div0=document.querySelector("#div0");
div0.style.width="100px";
div0.style.height="100px";
div0.style.border="1px solid #000000";
div0.style.backgroundColor="#FF0000";
// 上面的对象写法，需要将所有的css中-字母 替换为大写字母
// 例如  font-size    fontSize
// 而style字符串方式写法，按照原css行内样式填写

div0.style="width:100px;height:100px;background-color:red"
```

【注】设置element:HTMLElment,编译器跳出提示，是ts的格式

```
// Object.assign(target, source)  复制对象  浅复制
var o={a:1,b:2};
var o1={};
Object.assign(o1,o);
o.a=10;
console.log(o,o1);

//给div0增加样式
Object.assign(div0.style,{
    width:"50px",
    height:"50px",
    backgroundColor:"red"
})
```

```
// 增添class样式
div0.className="div1";
div0.className+=" div2";

//删除单个class样式
div0.className=div0.className.replace("div1","");
```

【注】

- 如果DOM的行内样式有内容，可以通过这个方式获取对于的行内样式
- 如果DOM的样式在CSS中，这时候还没有渲染所以无法计算CSS的样式，这种style获取是不能获得CSS样式的

```
console.log(div0.style.width);
```

##### 获取计算后的dom样式

​	ie

- currentStyle

```
console.log(div0.currentStyle.width);
```

​	非ie

- 想要获取计算后样式，就需要使用getComputedStyle获取元素的样式，不持支IE8及以下

```
console.log(getComputedStyle(div0).width);
//getComputedStyle先做了css行内样式和dom整合，然后计算
```

【注】兼并ie和非ie

```
var style;
try{
    style=getComputedStyle(div0);//先尝试这个
}catch(error){
    style=div0.currentStyle;//上面不行就运行这个
}
```

document.styleSheets

​		获取CSS中的样式

```
for(var i=0;i<document.styleSheets[0].cssRules.length;i++){
    console.log(document.styleSheets[0].cssRules[i].selectorText)
     for(var j=0;j<document.styleSheets[0].cssRules[i].style.length;j++){
         var key=document.styleSheets[0].cssRules[i].style[j];
         //console.log(key,document.styleSheets[0].cssRules[i].style[key]);
         if(document.styleSheets[0].cssRules[i].selectorText===".div2"){
             document.styleSheets[0].cssRules[i].style.color="green";
         }
     }
}
```

​		添加CSS样式

```
var styles={
    ".div1":{
        width:"50px",
        height:"50px",
        backgroundColor:"red"
    },
    ".div2":{
        fontSize:"20px",
        color:"#FFFFFF"
    }
 }

init();
function init(){
     var style=document.createElement("style");
     document.head.appendChild(style);
     var styleSheet=document.styleSheets[document.styleSheets.length-1];
     for(var prop in styles){
         addCss(styleSheet,prop,styles[prop]);
     }
 }

 function addCss(styleSheet,selector,style){
     // console.log(styleSheet,selector,style)
     // console.log(styleSheet.insertRule)
     var str=selector+" {";
     for(var prop in style){
         var value=style[prop]
         prop=prop.replace(/([A-Z])/g,function($1){
             return "-"+$1.toLowerCase();
         })
         str+=prop+":"+value+";"
     }
     str+=" }";
     styleSheet.insertRule(str,cssRules.length);
     //insertRule(rule,index); index是下标；
 }
 
封装js
setStyle:function(styles){
    var style=document.createElement("style");
    document.head.appendChild(style);
    var styleSheet=document.styleSheets[document.styleSheets.length-1];
    for(var prop in styles){
        this.addCss(styleSheet,prop,styles[prop]);
    }
},
addCss:function(styleSheet,selector,style){
    var str=selector+" {";
    for(var prop in style){
        var value=style[prop]
        prop=prop.replace(/([A-Z])/g,function($1){
            return "-"+$1.toLowerCase();
        })
        str+=prop+":"+value+";"
    }
    str+=" }";
    styleSheet.insertRule(str,styleSheet.cssRules.length);
}
```

#### Dom对象的常见属性

##### 宽高

clientWidth	clientHeight  客户宽高

offsetWidth	offsetHeight  偏移宽高

scrollWidth	scrollHeight  滚动内容宽高



DOM的宽高问题

```
console.log(div.clientWidth,div.clientHeight);
//计算后宽高=宽高+padding-(如果有滚动条，减去滚动条宽高)

console.log(div.offsetWidth,div.offsetHeight);
//计算后宽高=宽高+padding+border

console.log(div.scrollWidth,div.scrollHeight);
//1、如果没有超出，等同于clientWidth和clientHeight
//2、如果超出，就是实际内容所占的宽高，但是padding没有右侧和下侧的
//3、如果超出，就是实际内容所占的宽高，但是padding没有右侧和下侧的-(如果有滚动条，减去滚动条宽高)
```

 html和body宽高问题

- document.documentElement   html标签
- document.body    body标签

【注】body标签不会因为宽度撑开变化，但是会因滚动条变化

​		body：

```
console.log(document.body.clientWidth,document.body.clientHeight);
//实际body的宽度和高度-滚动条宽高

console.log(document.body.offsetWidth,document.body.offsetHeight);
//实际body的宽度和高度-滚动条宽高

console.log(document.body.scrollWidth,document.body.scrollHeight);
//实际body中内容的宽高
```

​		html：

```
console.log(document.documentElement.clientWidth,document.documentElement.clientHeight);
//当前文档的可视宽高-(如果有滚动条，减去滚动条宽高)

console.log(document.documentElement.offsetWidth,document.documentElement.offsetHeight);
//当前文档的内容宽高-(如果有滚动条，减去滚动条宽高)

console.log(document.documentElement.scrollWidth,document.documentElement.scrollHeight);
//当前文档的可视宽高，如果有滚动条，就是实际body撑开的宽高
```

##### 位置

clientLeft	clientTop  客户位置

offsetLeft	offsetTop  偏移位置

scrollLeft	scrollTop  滚动条位置



DOM的位置问题

```
console.log(div2.clientLeft,div2.clientTop);
//边框线的宽高

console.log(div2.offsetLeft,div2.offsetTop);
//当前div到父容器左上角的距离（父容器是定位），它和position的left和top是相同的

console.log(div2.scrollLeft,div2.scrollTop);
//当前元素的滚动条位置，前面的这些属性都是只读，但是这个是可以修改的
div2.scrollLeft=100;//滚动条位置设置

var rect=div2.getBoundingClientRect();
console.log(rect);
// rect.x===rect.left;
// rect.y===rect.top;   当前元素到可视窗口左上角的位置
```

 html和body位置问题

- clientLeft ,offsetLeft 不考虑
- 页面中的滚动是html的scrollTop和scrollLeft控制，早期的浏览器是body控制

#### 应用

​		找徐峥

```
js封装
var Utils=(function(){
	return {
        ce:function(type,style,parent){
            var elem=document.createElement(type);
            if(style){
                for(var prop in style){
                    elem.style[prop]=style[prop];
                }
            }
            if(typeof parent==="string") parent=document.querySelector(parent);
            if(parent) parent.appendChild(elem);
            return elem;
        }
	}
})();


var n = 2,
arr = [];
init();
function init() {
createImageCon(n);
}

function createImageCon(n) {
/*  document.querySelector("div").innerHTML="";
arr.length=0; */
for (var i = 0; i < arr.length; i++) {
    arr[i].remove();
    arr[i] = null;
}
arr.length = 0;
for (var i = 0; i < n * n; i++) {
    var img = Utils.ce("img", {
        width: 500 / n + "px",
        height: 500 / n + "px",
    });
    if (i === 0) img.src = "img/1.png";
    else img.src = "img/2.png";
    arr.push(img);
    img.addEventListener("click", clickHandler);
	}
    arr.sort(function () {
        return Math.random() - 0.5;
    })
    .forEach(function (item) {
        document.querySelector("div").appendChild(item);
    });
}

function clickHandler(e) {
if (this.src.indexOf("1.png") > -1) {
    n++;
}
createImageCon(n);
}
```

​		标题字体滚动

```
var str="欢迎同学们来千锋好程序员学习H5的课程。";
var i=0;
setInterval(animation,400);

function animation(){
    i++;
    if(i>str.length-1) i=0;
    document.title=str.slice(i);
}
```

​		给执行元素列表中的内容增加外容器

```
//每个元素外面增加
function warp(elemType,newType){
    var elems=document.querySelectorAll(elemType);
    elems.forEach(function(item){
        var parent=document.createElement(newType);
        item.parentElement.insertBefore(parent,item);
        parent.appendChild(item);
    })
}
warp("span","div");

//整个相同元素外面增加
function warpAll(elemType,newType){
    var elems=document.querySelectorAll(elemType);
    if(elems.length===0) return;
    var parent=document.createElement(newType);
    elems[0].parentElement.insertBefore(parent,elems[0]);
    elems.forEach(function(item){
        parent.appendChild(item);
    })
}
warpAll("span","div");
```

​		七彩色方块

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>

    <script>
      var div,
        speed=10,
        arr=[
      "rgb(255,0,0)",
        "rgb(255,0,255)",
        "rgb(0,0,255)",
        "rgb(0,255,255)",
        "rgb(0,255,0)",
        "rgb(255,255,0)",
        "rgb(255,0,0)"
      ];

      init();
      function init() {
        divs = document.querySelectorAll("div");
        for (var i = 0; i < divs.length; i++) {
          Object.assign(divs[i].style, {
            width: "50px",
            height: "50px",
            border: "1px solid #000000",
            backgroundColor: arr[i],
          });
          divs[i].status=(i+1).toString();
          divs[i].arr = divs[i].style.backgroundColor
            .split("(")[1]
            .slice(0, -1)
            .split(",");
        }

        setInterval(animation, 16);
      }

      function animation() {
            for(var i=0;i<divs.length;i++){
                setColor(divs[i]);
            }
      }

      function setColor(div) {
        switch (div.status) {
          case "1":
            if (changeArr(div.arr, 2, true)) return (div.status = "2");
            break;
          case "2":
            if (changeArr(div.arr, 0, false)) return (div.status = "3");
            break;
          case "3":
            if (changeArr(div.arr, 1, true)) return (div.status = "4");
            break;
          case "4":
            if (changeArr(div.arr, 2, false)) return (div.status = "5");
            break;
          case "5":
            if (changeArr(div.arr, 0, true)) return (div.status = "6");
            break;
          case "6":
            if (changeArr(div.arr, 1, false)) return (div.status = "1");
            break;
        }
        div.style.backgroundColor = "rgb(" + div.arr.join(",") + ")";
      }

      function changeArr(arr, i, bool) {
        if (bool) {
          if (Number(arr[i])>= 255) {
            return true;
          }
          arr[i] = Number(arr[i]) + speed;
        } else {
          if (Number(arr[i])<= 0) {
            return true;
          }
          arr[i] = Number(arr[i]) - speed;
        }
        return false;
      }

      /*  rgb(255,0,0);
        rgb(255,0,255);
        rgb(0,0,255);
        rgb(0,255,255);
        rgb(0,255,0);
        rgb(255,255,0);
        rgb(255,0,0); */
    </script>
  </body>
</html>

```

​		滑动条位置

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #div0
        {
            width: 50px;
            height: 50px;
            background-color: rgba(50,50,50,0.3);
            position: fixed;
            right:100px;
            bottom: 100px;
            font-size: 40px;
            line-height: 65px;
            text-align: center;
            user-select: none;
            display: none;
            z-index: 999;
        }
    </style>
</head>
<body>
    <div id="div0">^</div>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksdsdalsdkalskdsal<br>
    aslkdjaskldjsalkdjaskldjaslkd<br>
    aslkdjaskldjsa<br>
    aslkdjaskldjsasadkjwioqdioqwoiqwoeiuwqoieuqwoi<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    aslkdjaskldjsasadkjwioqdiosadlaksd<br>
    <script>
        var div,bool=false,speed=200;
        init();
        function init(){
            div=document.querySelector("div");
            document.addEventListener("scroll",scrollHandler);
            div.addEventListener("click",clickHandler);
            setInterval(animation,16);
        }

        function scrollHandler(e){
            if(document.documentElement.scrollTop>document.documentElement.clientHeight){
                div.style.display="block";
            }else{
                div.style.display="none"
            }
        }

        function clickHandler(e){
            bool=true;
        }

        function animation(){
            if(!bool) return;
            if(document.documentElement.scrollTop<=0) bool=false;
            document.documentElement.scrollTop-=speed;
        }
    </script>
</body>
</html>
```

​		轮播图（一）

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .imgCon
        {
            width: 900px;
            height: 300px;
            background-image: url(./img/a.jpeg);
            background-size: 100% 100%;
            position: relative;
            left:0;
            right: 0;
            margin: auto;
            transition: all 0.5s;
        }
        .imgCon img
        {
            position: absolute;
            right: 20px;
            width: 80px;
            height: 50px;
            border:2px solid rgba(255,0,0,0);
        }
    </style>
</head>
<body>
    <div class="imgCon">
        <img src="./img/icon_a.jpeg">
        <img src="./img/icon_b.jpeg">
        <img src="./img/icon_c.jpeg">
        <img src="./img/icon_d.jpeg">
        <img src="./img/icon_e.jpeg">
    </div>

    <script>
            var imgCon,imgArr,pre;
            var gap=5;
            init();
            function init(){
                imgCon=document.querySelector(".imgCon");
                imgArr=Array.from(imgCon.children);
                imgArr.forEach(function(item,index){
                    item.style.top=gap+(54+gap)*index+"px"
                    if(index===0) changePre(item);
                    item.addEventListener("click",clickHandler);
                })
            }


            function clickHandler(e){
                changePre(this);
                imgCon.style.backgroundImage="url("+this.src.replace("icon_","")+")";
            }


            function changePre(elem){
                if(pre){
                    pre.style.borderColor="rgba(255,0,0,0)";
                }
                pre=elem;
                pre.style.borderColor="#ff9d00";
            }
    </script>
</body>
</html>
```

​		轮播图（二）

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
         #carousel
        {
            width: 900px;
            height: 300px;
            position: relative;
            left:0;
            right: 0;
            margin: auto;
            overflow: hidden;
        }
        .imgCon
        {
            width: 4500px;
            height: 300px;
            position: absolute;
            font-size: 0;
            transition: all 0.5s;
            left:0;
        }
        .imgCon>img
        {
            width:900px;
            height: 300px;
           
        }
        .left,.right
        {
            position: absolute;
            top:120px;
        }
        .left{
            left:20px;
        }
        .right{
            right:20px;
        }
        ul
        {
            position: absolute;
            bottom: 20px;
            list-style: none;
            margin: 0;
            padding: 0;
        }
        ul>li
        {
            float: left;
            width: 16px;
            height: 16px;
            border-radius: 16px;
            border:1px solid #FF0000;
            background-color: rgba(255,0,0,0);
            margin-left: 10px;
        }
        ul>li:first-child
        {
            margin-left: 0;
        }
    </style>
</head>
<body>
    <div id="carousel">
        <div class="imgCon">
            <img src="./img/a.jpeg">
            <img src="./img/b.jpeg">
            <img src="./img/c.jpeg">
            <img src="./img/d.jpeg">
            <img src="./img/e.jpeg">
        </div>
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
        <img class="left" src="./img/left.png">
        <img class="right" src="./img/right.png">
    </div>
    <script>

        var imgCon,left,right,ul,liArr,pre;
        var pos=0;
        init();
        function init(){
            imgCon=document.querySelector(".imgCon");
            left=document.querySelector(".left");
            right=document.querySelector(".right");
            ul=document.querySelector("ul");
            liArr=Array.from(ul.children);
            ul.style.left=(imgCon.parentElement.offsetWidth-ul.offsetWidth)/2+"px";
            left.addEventListener("click",clickHandler);
            right.addEventListener("click",clickHandler);
            liArr.forEach(function(item){
                item.addEventListener("click",dotClickHandler);
            });
            changePre();
        }

        function clickHandler(e){
            if(this===left){
                pos--;
                if(pos<0) pos=imgCon.children.length-1;
            }else{
                pos++;
                if(pos>imgCon.children.length-1) pos=0;
            }
            imgCon.style.left=-pos*900+"px";
            changePre();
        }

        function dotClickHandler(e){
            pos=liArr.indexOf(this);
            imgCon.style.left=-pos*900+"px";
            changePre();
        }

        function changePre(){
            if(pre){
                pre.style.backgroundColor="rgba(255,0,0,0)";
            }
            pre=liArr[pos];
            pre.style.backgroundColor="rgba(255,0,0,0.3)";
        }
    </script>
</body>
</html>
```
