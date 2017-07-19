# The Elegance of JavaScript

主要用来督促自己学习JavaScript

## 一、基本语法
### 1.语句
- JavaScript程序的执行单位为行（line），一行一行执行；
### 2.变量
#### 2.1概念
- 变量是对‘值’的引用，变量等同于引用一个值;
- 变量的声明和赋值分为两个部分：
```js
var a = 1;
```
 相当于：
```js
var a;
a = 1;
```
- 如果只声明变量而不赋值，变量值为undefined（无定义）；
- 变量赋值时，忘记写var声明，这条语句也是有效的：<br>
var a = 1 与 a = 1不完全一样，主要体现在delete命令无法删除前者,不写var不利于表达意图，而且容易不知不觉的创建全局变量；
- 如果一个变量没有声明就直接使用，JavaScript会报错（ReferenceError: ... is not defined）;
- 在同一条var命令中可以声明多个变量：var: a,b;
- 使用var声明一个已经存在的变量，是无效的：<br>
```js
var a = 1;
var a;
a //1
```
- 如果第二次声明的同时还进行了赋值<br>
```js
var a = 1;
var a = 2;
a //2
```
 上面的代码等同于：<br>
```js
var a = 1；
var a；
a = 2;
```
#### 2.2变量提升
- JavaScript引擎的工作方式：先解析代码，获取所有被声明的变量，然后逐行运行，造成所有变量的声明语句，都会提升到代码头部（变量提升）；
```js
 console.log(a)
 var a = 1;
 ```
 等于：
```js
var a;
console.log(a)
a = 1;
```
上面代码使打印出来的a为undefined；
### 3.标识符
- 标识符：用来识别具体对象的一个名称，JavaScript语言的标识符大小写敏感
- 规则：<br>
(1) 第一个字符可以是任意Unicode字母（包括英文字母和其他语言字母），以及美元（$）和下划线（_）;<br>
(2) 第二个字符以及后面的字符，除了以上的字符外，还可以是0-9之间的数字。
(3) 标识符的第一字符不可以为数字，不可以含有*，+，-；
(4) 中文字符可以作为变量名，JavaScript的保留字不可以作为变量名；
### 4.注释
- JavaScript注释分为：单行注释和多行注释；
```js
//单行注释
/*
a
b
多行注释
*/
```
- 由于历史上JavaScript兼容HTML代码注释，所以<!--和-->也被视为单行注释；
```js
x = 1;<!-- x = 2;
--> x = 3;
```
上面的代码只有x = 1会执行到，其他部分被注释了，-->只有位于行首才会被当成单行注释，否则为运算符
```js
function Down(n) {
  while(n --> 0){
    console.log(n);
  }
}
Down(3)
//2
//1
//0
```
### 5.区块
- JavaScript使用大括号将相关语句结合到一起成为区块（block）；
- JavaScript的区块不构成单独的作用域。
```js
{
 a = 1;
}
a //1
```
### 6.条件语句
#### 6.1 if结构
```js
if(expression) 
  statement;
// or
if(expression) statement;
// or 
if(expression) {
 statement;
}
```
#### 6.2if...else结构
```js
if(m === 3){
 //then
} else {
  //else
}

if(m == 1){
 //...
} else if(m == 2){
 //..
} else if(m == 3){
 //..
} else {
 //..
}
```
- else总是跟随离自己最近的那个if语句：
```js
  var m = 1;
  var n = 2;
  if(m !== 1)
  if(n === 2) console.log('hello');
  else console.log('world');
  //相当于
  if(m !== 1){
     if(n === 2){
       console.log('hello');
     }else {
       consloe.log('world');
     }
  }
```
#### 6.3 switch结构
- 多个if...lese一起用的时候，可以使用更方便的switch结构；
```js
switch(fruit){
   case: 'apple':
     //...
     break;
   case: 'cherry':
     //...
     break;
   default:
     //...
}
// 每个case代码块内部的break语句都不能少，否则会据需执行下一个case块，不会跳出switch语句
```
- switch语句部分和case语句部分可以使用表达式
```js
switch(2+2){
  case 1+3:
    f();
    break;
  default:
     neverhappens();//永远不会执行到
}
```
- switch语句后面的表达式与case后面的表达式进行比较运算时，采用的是严格相等运算符（===），比较时不会发生类型转换;
```js
  var x = 1;
  switch(x){
    case true:
      console.log('x的类型发生了转化');
      break;
    default:
       console.log('x没有发生类型转化');
  }
```
#### 6.4三元运算符?:
- 三元运算符结构:(condition)?one:two,如果condition为true，返回one，否则返回two；

### 7.循环语句
#### 7.1while循环
- while语句包括一个条件语句和待执行代码块
```js
  while(expression) 
    statement;
  //or
  while(expression) statement;
  //or 
  while(expression){
    statement;
  }
```
#### 7.2for循环
- for语句是循环的另一种形式：可以指定起点、终点、终止条件；
```js
  for(initialize;test;increment)
    statement;
    //or
  for(initialize;test;increment){
    statement;
  }
```
- 初始表达式（initialize）：确定循环的初始值，只在循环开始时执行一次；
- 测试表达式（test）：检查循环条件，只要为真进行后续操作；
- 递增表达式（increment）：完成后续操作，返回上一步，再次进行检查循环条件；
##### demo:
```js
  var x = 3;
  for(var i=0;i<x;i++){
    console.log(i)
  }
  //0
  //1
  //2
```
- for语句的三个部分（initailize,test,increment）,可以省略任意其一，也可也省略全部；
```js 
  for(;;){
    console.log('Hello World !');
  }//此循环是个无限循环
```
#### 7.3do...while循环
- do...while循环与while循环类似，区别是：do...while循环先运行一次，然后判断循环条件；
```js
  do
    statement
  while(expression);
  //or
  do{
    statement
  } while(expression);
```
#### 7.4break和continue语句
- break和continue语句都有跳转作用，可以让代码不按既有顺序执行；
- break用于跳出代码模块或循环；
```js
  var i = 0;
  while(i<100){
    console.log('i当前为：'+ i)；
    if（i === 10）break;
  }
```
- continue语句用于立即终止本轮循环，返回循环结构的头部，进行下一轮循环；
```js
  var i = 0;
  while(i < 20){
    i++;
    if(i%2 === 0) continue;
    console.log('i当前为：' + i);
  }
```
#### 7.5标签label
-label的格式如下：
```js
label: 
  statement
```
- label通常与break语句和continue语句配合使用，跳出待定的循环：
```js
  top:
  for(var i=0;i<3;i++){
    for(var j=0;j<3;j++){
      if(i === 1 && j ===1) break top;
      console.log('i=' +i + ' , j=' + j);
    }
  }
  // i=0, j=0
  // i=0, j=1
  // i=0, j=2
  // i=1, j=0
  
  top: 
  for(var i=0;i<3;i++){
    for(var j=0;j<3;j++){
      if(i === 1 && j ===1) continue top;
      console.log('i=' +i + ' , j=' + j);
    }
  }
  // i=0, j=0
  // i=0, j=1
  // i=0, j=2
  // i=1, j=0
  // i=2, j=0
  // i=2, j=1
  // i=2, j=2
  top: 
  for(var i=0;i<3;i++){
    for(var j=0;j<3;j++){
      if(i === 1 && j ===1) continue;
      console.log('i=' +i + ' , j=' + j);
    }
  }//如果上面continue后面没有top标签，那么下一轮的内循环
  // i=0, j=0
  // i=0, j=1
  // i=0, j=2
  // i=1, j=0
  // i=1, j=2
  // i=2, j=0
  // i=2, j=1
  // i=2, j=2
```

## 数据类型
### 1.概述
- JavaScrip的每一个值，都有自己的数据类型，分别为：数值（number）、字符串（string）、布尔值（boolean）、undefined、null、对象（object）；
- 通常我们将数值、字符串、布尔值称为原始类型，将对象称为合成类型，undefined和null为特殊值；
- 对象又可以分为三个子类型：狭义的对象（object）、数组（array）、函数（function）；
### 2.typeof运算符
- JavaScript有三种方法确定一个值属于什么类型：typeof运算符、instanceof运算符、object.prototype.toString方法；
```js
  typeof 123 //"number"
  typeof '123' //"string"
  typeof true //"boolean"
  function f(){}
  typeof f //"function"
  typeof undefined //"undefined"
  typeof window //"object"
  typeof {} // "object"
  typeof [] // "object"
  typeof null //"object"
  ```
  - 数组是特殊的对象，null也属于object（历史遗留问题），null本质上是类似于undefined的特殊值；
  - 区分数组（array）和对象（object）；
  ```js
    var o = {};
    var a = [];
    o instanceof Array //false
    a instanceof Array //true
  ```
  ### 3.null和undefined
  #### 3.1概述
  - null和undefined都表示‘没有’，含义非常相似
  - 在if语句中，null和undefined都会被自动转化为false，相等运算符（==），两者相等
  ```js 
   null == undefined; //true
   Number(null); //0
   5 + null; //5
   Number(null); //NaN
   5 + null; //NaN
 ```
 - null表示“无”的对象，转化为数字为0；undefined表示一个“无”的原始值，转化为数字是为NaN；
 #### 3.1用法和含义
 - null表示空值，调用函数时，摸个参数未设置任何值，此时传入的值为null；
 - undefined表示未定义；
 ### 4.布尔值
 - 布尔值分为真（true）假（false）两个状态；
 - 下列运算符会返回布尔值：
 >两元运算符：&&（And），||（Or)<br>
 >前置逻辑运算符：！（Not）<br>
 >相等运算符： === ，== ，！==， ！=<br>
 >比较运算符:>, >=, <, <=<br>
 - 如果JavaScript预期某个位置应该为布尔值，会将该位置上的值自动转化为布尔值，undefined，null，false，0，NaN，"",''会被转化为false，其他值都视为true；
 ```js
   if(''){
     console.log(true);
   }//没有输出
   if({}){
    console.log(true);
   }//true
 ```
 
 ## 数值
 ### 1.概述
 #### 1.1正数和浮点数
 - JavaScript内部，所有的数字都是以64位浮点数形式存储的；
 - 由于浮点数不是精确的值，所以计算小数是会出现意外
 ```js
   1 === 1.0 //true
   0.1 + 0.2 === 0.3; //false
   0.3 / 0.1 // 2.9999999999999996
```
#### 1.2数值精度
- 根据国际IEEE 754标准，JavaScript浮点数的64位二进制，从左边开始：
>第1位：符号位，0表示正数，1表示负数<br>
>第2位到第12位：指数部分<br>
>第13位到第64位：小数部分（有效数字）<br>
- 符号位决定了一个数的正负，指数为决定了数值的大小，小数位决定了数值的精度。
#### 1.3数值范围
- 根据标准，64位浮点数的指数部分的长度是11位的2进制，意味着指数部分的最大值是2047（2的11次方减1）；也就是说，64位浮点数的指数部分最大为2047，分出一半表示负数，JavaScript表示的是指范围是（2^-1023—2^1024),超出这个范围的数值无法表示；
- 如果指数部分超过最大值1024，JavaScript会返回Infinity（正向溢出）；如果等于或超过最小值-1023，JavaScript会把这个数转化为0（负溢出）；
```js
  var a = 0.5;
  for(var i=0;i<25;i++){
    x = x*x;
  }
  x //0;
  //上面代码对0.5连续做25次平方，超出了可表示的范围，JavaScript将其转化0；
```
### 2.数值的表示方法
- JavaScript有多种数值表示方式，例如11（10进制），0xFF（16进制）；
- 数值也可以使用科学计数法来表示：
```js
  123e3 //123000
  123e-3 //0.123
```
- 在下面情况下，JavaScript会将数值自动转化为科学计数法表示；
< 小数点前数字多于21位
```js
 1234567890123456789012
 // 1.2345678901234568e+21
```
< 小数点后紧跟5个0以上：
```js
  0.0000001 // 1e-7
  //否则按原来表达
  0.000001 // 0.000001
```
### 数值的进制
- JavaScript对整数有四种进制表示方法：十进制，十六进制，八进制，二进制；
>十进制：没有前导0的数值<br>
>八进制：有前缀0o或0O的数值，或者有前导0、且只用到0-7的阿拉伯数字的数值<br>
>十六进制：有前缀0x或0X的数值<br>
>二进制：有前缀0b或0B的数值<br>

### 特殊数值
#### 4.1正零和负零
- 在JavaScript内部，实际上存在两个0，+0和-0；
```js
  -0 === +0 //true
  0 === -0 //true
  0 === +0 //true
```
- 几乎所有场合，+0和-0都会被当做正常的零来处理，唯一区别是作为分母的时候：
```js
  +0 //0
  -0 //0
  (-0).toString() //'0'
  (0).toString() //'0'
  (1/-0) === (1/+0) //false
  // 1/-0得到的是-Infinity，1/+0得到的是+Infinity
```
#### 4.2NaN
- NaN是JavaScript的特殊值，表示非数字（Not a Number）,主要出现在字符串解析成数字出错的场合；
```js
  5 - 'x' //NaN
  5 - '4' //1
  //上面的代码运行时，会自动将字符串x转化为数字，由于x不能转化为数字，最后结果为NaN
```
- 一些函数运算结果会出现NaN,0/0得到NaN
```js
  Math.acos(2) //NaN
  Math.log(-1) //NaN
  Math.sqrt(-1) //NaN
  0/0 //NaN
```
- NaN不是一种独立的数据类型，而是一个特殊值，依然属于Number
```js
  typeof NaN //'number'
```
- NaN不属于任何值，包括自己本身
```js
  NaN === NaN //false
```
- NaN在布尔运算时被当做false：
```js
  Boolean(NaN) //flase
```
- NaN与任何数运算都为NaN
- 可以使用isNaN来判断一个值是否为NaN；
```js
  isNaN(NaN) //true
  isNaN(123) //false
  isNaN('Hello') //true
  //相当于
  isNaN(Number('Hello')) //true
```
- 对于对象和数组，isNaN返回true：
```js
  isNaN({}) //true
  isNaN(['xyz']) //true
```
- 对于空数组和只有一个数值成员的数组，isNaN返回false
```js
  isNaN([]) //false
  isNaN([123]) //false
  isNaN(['123']) //false
```

  















