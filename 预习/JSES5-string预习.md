## JSES5-string 

### 严格模式

#### HTML_严格模式与混杂模式 

Doctype可声明三种DTD类型，分别表示严格版本、过渡版本以及基于框架的 HTML 文档。 

> 在标准模式中，又称严格模式，是指浏览器按照 W3C 标准解析代码 

> 在混杂模式中，页面以一种比较宽松的向后兼容的方式显示。混杂模式通常模拟老式浏览器的 行为以防止老站点无法工作。 

##### 浏览器根据DOCTYPE是否存在以及使用的哪种DTD来选择要使用的呈现方法。 

> 如果XHTML、HTML 4.01文档包含形式完整的DOCTYPE，那么它一般以标准模式呈现。 
>
> 包含过渡DTD和URI的DOCTYPE也导致页面以标准模式呈现，但是有过渡DTD而没有URI会导致页面 以混杂模式呈现。 
>
> DOCTYPE不存在或形式不正确会导致HTML和XHTML文档以混杂模式呈现 

html5既然没有DTD，也就没有严格模式与宽松模式的区别，html5有相对宽松的语法，实现时，已经尽可 能大的实现了向后兼容。 

#### 严格模式

目的：

1.消除JS语法不合理、不严谨减少怪异行为 

2.消除代码不安全之处，保证代码运行安全 

3.提高编译运行效率 

4.为将来新版本JS做铺垫 

语法： “use strict” 

浏览器支持： 

IE10+ firefox 4+ Safari 5.1+ Chrome 

### ES5数组新方法 

#### indexOf  

作用：在数组中查找一个数所在的位置。

```javascript
var arr1 = [12,23,34,45,56,67];
console.log(arr1.indexOf(23)); //结果是1
```

#### forEach 

作用：对数组的每个元素做某个处理（函数的方式）

```javascript
var arr1 = [12,23,34,45,56,67];
arr1.forEach(alert);//显示数组的每个元素

```

tips:可以自定义匿名函数调取，然后对数组的每个元素进行处理。

foEach()函数的参数是个回调函数，forEach对应的回调函数有三个参数（数组元素内容，元素索引，数组本身） 

```javascript
arr1.forEach(arrInc);
function arrInc(num,index,arr){
arr[index] = num+1; //每个元素都加1
}
```



函数也是引用类型，跟数组一样，函数名和数组名都是保存着地址。 

tips:回调函数就是一个通过函数指针(地址)调用的函数。如果你把函数的指针（地址）作为参数传递给另一个函数，当 这个指针被用来调用其所指向的函数时，我们就说这是回调函数。 

回调函数不是由该函数的实现方直接调用，而是在特 定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应。 

就是说你先按要求提供一个函数给某个方法，在合适时候这个方法会去调用你提供的自定义函数。 

#### map

作用：把原始数组的每个元素进行某种处理后，产生（映射）一个新的数组。回调函数参数是数组元素本身。 

```java
var arr1 = [12,23,34,45,56,67];
var arr2 = arr1.map(arrSqr);
function arrSqr(num){
return num*num
}

```

注意：map最后产生（映射）出了一个新的数组，原数组没有变化，需要重新设置数组（地址）接受这个新数组。

#### filter

作用：就是字面上过滤的意思，根据条件过滤数组的元素，filter的回调函数需要返回的是boolean类型的值（最好是关系判断的结果，比如大小，等于，不等于）。 

```javascript
var arr1 = [-12,23,-34,45,-56,67];
var arr2 = arr1.filter(eqZero); //过滤掉所有小于等于0的数，留下大于0的数
function eqZero(num){
return num>0;
}
```

浏览器支持：

Opera 11+ fireFox 3.6+ Chrome 8+ iE 9+ Safari 5+ 

注意：filter也是重新生成了新的数组，需要新的地址来接收（一一对应？）

### 字符串概念和定义 

字符串就是一串字符，由双（单）引号括起来。字符串是 JavaScript 的一种基本的数据类型。 

#### 基本类型

var str ="亲";           

定义一个字符串变量str，内容为“亲”

#### 引用类型

var str="new Srting("hello");

定义一个字符串变量str，内容为hello，

注意此刻str为object(对象)类型 用new产生的变量都是引用类型的变量，也叫对象。 

```javas
var s1 = "string";
var s2 = new String("string");
console.log(typeof(s1)); //输出的是 string
console.log(typeof(s2)); //输出的 object
```

#### 字符串的常用属性和函数 

length：表示字符串的长度； 

```javascript
如 : var str=“how are you”;
 alert(str.length);
```

字符串的函数（方法）--字符串的获取方法

charAt(3) //获取下标为3的字符 

charCodeAt(3) //获取下标为3的字符的编码 

fromCharCode(94) //编码转换成字符 

注意：该方法是string的静态方法，所以用string调用

例子：

```javasc
String.fromCharCode(98,99);
```



### 字符集 

#### 字符编码

ASCII（美国信息交换标准代码）是基于拉丁字母的一套电脑编码系统，主要用于显示现代英语和其他西欧语言 

注意;0-48;  A-65;a-97;

并且比较大小时默认比较首位的大小，然后次之进行排序

GBK 共收录了21003个汉字，英文使用单字节编码，兼容ASCII编码，中文部分采用双字节编码。 

Unicode为每种语言中的每个字符设定了统一并且唯一的二进制编码，以满足跨语言、跨平台进行文本转换、处理的要求。 

UTF-8是一种针对Unicode的可变长度字符编码。用在网页上可以统一页面显示中文简体繁体及其它语言。 

#### 字符串的查找方法

indexOf("abc") 

查找字符串第一次出现的位置//

lastIndexOf("abc")  

查找字符串最后一次出现的位置 如果没找到 返回-1 // 

##### search办法

```javascript
search() 正则匹配 (返回索引位置，没有找到就返回-1)
function test(){
var str = "what Are you 弄啥哩!";
/*
var strNew = str.search("are");
document.write(strNew); //显示-1；因为，区分大小写
*/
var strNew = str.search(/are/i); //用正则表达式，i表示不区分大小写
document.write(strNew); //显示5；因为，不区分大小写
}

```

#### match办法



### 字符串常见API 



