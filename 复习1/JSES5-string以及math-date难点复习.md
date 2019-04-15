# JS-String以及Math难点复习

## JS-String

### 严格模式

#### HTML_严格模式与混杂模式 

Doctype可声明三种DTD类型，分别表示严格版本、过渡版本以及基于框架的 HTML 文档。 

当浏览器厂商开始创建与标准兼容的浏览器时，他们希望确保向后兼容性。为了实现这一点，他们 创建了两种呈现模式：标准模式和混杂模式 。

在标准模式中，又称严格模式，是指浏览器按照 W3C 标准解析代码 

在混杂模式中，页面以一种比较宽松的向后兼容的方式显示。混杂模式通常模拟老式浏览器的 行为以防止老站点无法工作。 

#### 严格模式的目的

>消除JS语法不合理、
>
>不严谨减少怪异行为 消除代码不安全之处，
>
>保证代码运行安全 
>
>提高编译运行效率 为将来新版本JS做铺垫 

浏览器支持：IE10+ firefox 4+ Safari 5.1+ Chrome 

### ES5数组新增的常见办法

#### indexOf  

作用：数组中查找一个数所在的位置， 

```javascript
var arr1 = [12,23,34,45,56,67];
console.log(arr1.indexOf(23)); //结果是1
```

#### forEach  

作用：对数组的每个元素做某个处理（函数的方式） 。

```javascript
var arr1 = [12,23,34,45,56,67];
arr1.forEach(alert);//显示数组的每个元素
```



重点：forEach()函数的参数是个回调函数，forEach对应的回调函数有三个参数（数组元素内容，元素索引，数组本身） 

```javascript
var arr=[12,23,34,45];
	arr.forEach(arrInc);//把数组arr的每个元素做arrInc处理
	console.log(arr);
arrInc：所做处理就是给元素加1
arr13:所做处理就是每个元素乘以1.3
function arrInc(num,index,arr){
	arr[index] = num+1;
}

function arr13(num,index,arr){
	// arr[index] = num*1.3;
	arr[index] = arr[index]*1.3;
}
```

回调函数就是一个通过函数指针(地址)调用的函数。 

#### map

作用：把原始数组的每个元素进行某种处理后，产生（映射）一个新的数组。 

回调函数参数是数组元素本身。 

```javascript
var arr1 = [12,23,34,45,56,67];
var arr2 = arr1.map(arrSqr);
function arrSqr(num){
return num*num
}
(注意：请记住回调函数将结果return)
```

#### filter

作用：过滤的意思，根据条件过滤数组的元素，

filter的回调函数需要返回的是boolean类型的值。 

```javascript
var arr1 = [-12,23,-34,45,-56,67];
var arr2 = arr1.filter(eqZero); //过滤掉所有小于等于0的数，留下大于0的数
function eqZero(num){
return num>0;
}
```

### 字符串的定义和创建

定义：字符串就是一串字符，由双（单）引号括起来。 

#### 基本类型

var str=‘亲’；  

#### 引用类型

var str = new String(“hello”);  

注意：定义一个字符串变量str，内容为hello， 

注意此刻str为object(对象)类型 

用new产生的变量都是引用类型的变量，也叫对象。 

### 字符串的常用属性和函数 

#### length

```javascript
var str=“how are you”;
 alert(str.length);
输出是11
```

#### 字符串的函数（方法）--字符串的获取方法 

charAt(3)     //获取下标为3的字符 

```javascript
var s=str.charAt(3)
```



charCodeAt(3) //获取下标为3的字符的编码 

```javascript
var s=str.charCodeAt(3)
```

特殊的：

fromCharCode(94) //编码转换成字符 

```javascript
<script>
var str="hello world"
var s=String.fromCharCode(98,99);
;
alert(s);
alert(typeof s)
</script>
输出为bc
```

### 字符编码

#### ASCII（美国信息交换标准代码） 

是基于拉丁字母的一套电脑编码系统，主要用于显示现代英语和其他西欧语言。

#### GBK 

 共收录了21003个汉字，英文使用单字节编码，兼容ASCII编码，中文部分采用双字节编码。

#### Unicode 

为每种语言中的每个字符设定了统一并且唯一的二进制编码，以满足跨语言、跨平台进行文本转换、处理的要求。

#### UTF-8

是一种针对Unicode的可变长度字符编码。用在网页上可以统一页面显示中文简体繁体及其它语言。

 

### 字符串的属性和函数 

> 字符串的查找方法 indexOf("abc") 

> 查找字符串第一次出现的位置 lastIndexOf("abc") 查找字符串最后一次出现的位置 如果没找到 返回-1 

### search方法 

search() 正则匹配 (返回索引位置，没有找到就返回-1) 

注意：使用search查找可以使用正则表达式

```javascript
function test(){
var str = "what Are you 弄啥哩!";
/*
var strNew = str.search("are");
document.write(strNew); //显示-1；因为，区分大小写
*/
var strNew = str.search(/are/i); //用正则表达式，i表示不区分大小写
document.write(strNew); //显示5；因为，不区分大小写
}
小技巧：i表示不区分大小写，g表示这个为全局变量，将所有的are寻找出来
```

#### match方法

match () 方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配。该方法类似 indexOf() 和 lastIndexOf()，但是它返回指定的值，而不是字符串的位置。将匹配的内容存入数组 

重点：若在str里找得到，返回的是查找的字符，找不到，返回的值是null

#### replace办法

作用：替换字符串

```javascript
var str="how are you";
 document.write(str.replace("are","old are"));
```

注意：这里的替换只能执行一次，不能够进行全局匹配，而且区分大小写，如果需要全局匹配，则应使用 正则表达式： str.replace(/are/gi,“old are”) ：表示把str中所有的are，全部替换为 old are，g表示进行全局匹配， i表示匹配的时候忽略大小写； 

#### slice和substring方法 

作用：截取字符串

slice（start,end） 提取字符串的某个部分，并以新的字符串返回被提取的部分。 两个参数表示截取的开始下标和结束下标。 

substring(start,stop) 提取字符串中介于两个指定下标之间的字符，并以新的字符串返回被提取的部分。 两个参数表示截取的开始下标和结束下标。 

注意：截取都是包括开始的下标元素，但是不包括结束的下表元素

区别， slice参数支持负数（从后往前算），substring不支持 

#### split方法

作用：字符串分隔；

var str=“aaa1bbb1cc1d1”; 

var arr=str.split(“1”); 

### ==与=== 

===(恒等) 

1、如果类型不同，就[不相等] 

2、如果两个都是数值，并且是同一个值，那么[相等]。 

3、如果两个都是字符串，每个位置的字符都一样，那么[相等]；否则[不相等] 

4、如果两个值都是true，或者都是false，那么[相等]。 

5、如果两个值都引用同一个对象或函数，那么[相等]；否则[不相等]。 

6、如果两个值都是null，或者都是undefined，那么[相等]。 

==（等同） 

1、如果两个值类型相同，进行 === 比较。 

2、如果两个值类型不同，他们可能相等。根据下面规则进行类型转换再比较 

a、如果一个是null、一个是undefined，那么[相等]。 

b、如果一个是字符串，一个是数值，把字符串转换成数值再进行比较。 

c、如果任一值是 true，把它转换成 1 再比较；如果任一值是 false，把它转换成 0 再比较。 

d、任何其他组合，都[不相等]。 

## JS Math-Date

### Math对象的常用函数

Math.round(3.6) //四舍五入 

random() //返回0-1之间的随机数 

max(num1, num2) //返回较大的数 

min(num1, num2) //返回较小的数 

abs(num) //绝对值 

ceil(19.3) //向上取整“20” 

floor(11.8) //向下取整“11” 

pow(x,y) //x的y次方 

sqrt(num) //开平方 

### 三角函数（了解内容）

见w3c schol offier

### 随机数范围

从0到某个整数的随机数我们会。 任意两个整数之间的范围呢。 任意两个整数之间的随机数=取整（小数+随机数*（大数-小数）） function suiji(min,max){ var cha=max-min; var rund=Math.random()*cha; return min+parseInt(rund); } 

### 十进制转其它进制 

十进制转其他 ： var x=110; alert(x); 

alert(x.toString(8)); 

alert(x.toString(32)); 

alert(x.toString(16));  

### 创建日期对象 

Date对象用于处理日期和时间，Date对象记录着从1970年1月1日00:00:00开始以来的毫秒数。 

##### Date对象的定义 

​	var myDate=new Date() ;   //Date 对象自动使用当前的日期和时间作为其初始值。 

##### 创建Date对象同时指定日期和时间 

new Date("month dd,yyyy hh:mm:ss");

 new Date("month dd,yyyy"); 

new Date(yyyy,mth,dd,hh,mm,ss); 

new Date(yyyy,mth,dd); 

new Date(ms); 

获取时间

getDate() //返回天 

getDay() //返回星期几 ，从0开始 

getHours() //返回小时数 

getMinutes() //返回分钟数 

getMonth() //返回月份值 ，从0开始 

getSeconds() //返回秒数 

getTime() //返回完整的时间 ，毫秒数 

getFullYear() //返回年份 

设置时间： 

setDate() //改变Date对象的日期 

setHours() //改变小时数 

setMinutes() //改变分钟数 

setMonth() //改变月份，从0开始 

setSeconds() //改变秒数 

setTime() //改变完整的时间，毫秒数 

setYear() //改变年份 

##### 日期转换

字符串转换时间戳： 

Date.parse(日期字符串或日期对象) //返回自1970年1月1日起至参数日期止的毫秒数 

Date转为字符串

toTimeString() // 把 Date 对象的时间部分转换为字符串。 

toDateString() //把 Date 对象的日期部分转换为字符串。 

toUTCString() //根据世界时，把 Date 对象转换为字符串。 

toLocaleString() //根据本地时间格式，把 Date 对象转换为字符串。 

toLocaleTimeString() //根据本地时间格式，把 Date 对象的时间部分转换为字符串。

toLocaleDateString() //根据本地时间格式，把 Date 对象的日期部分转换为字符串。 

#### 封装自己的日期函数库dateUtil （明日必做）

#### 使用定时器

setInterval（回调函数，毫秒数）设置每隔指定的毫秒数执行一次回调函数，返回定时器编号。 

clearInterval（定时器编号）清除定时器设置。 

setTimeout（回调函数，毫秒数） 设置在指定的毫秒数后执行一次回调函数，返回定时器编号。 

clearTimeout （定时器编号）清除定时器设置。 

注意：注：因为只执行一次回调函数，所以为达到不停执行回调函数的效果必须在回调函数中再次设置。 