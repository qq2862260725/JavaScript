# The Elegance of JavaScript

主要用来督促自己学习JavaScript

## 一、基本语法
### 1.语句
- JavaScript程序的执行单位为行（line），逐行执行；
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
  ###  3.null和undefined
  ####  3.1概述
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
#### 4.3Infinity
- Infinity表示‘无穷’，表示整的数值太大，附属数值太小；
- 非0数值除以0得到Infinity；
```js
Math.pow(2,Math.pow(2,100)); //Infinity
0/0 //NaN
1/0 //Infinity
```
- Infinity有正负之分
- Infinity与NaN比较返回false
- Infinity与null运算时，null自动转化为0，与undefined计算时返回NaN
- isFinity返回一个布尔值，检查某个值是否为正常数值，而不是Infinity
```js
  isFinity(1) //true
  isFinity(Infinity) //false
```
### 5.与数值相关的全局方法
#### 5.1parseInt()
- parseInt()用于将字符串转化为数字
```js
  parseInt('123') //123
  parseInt('      123') //123
  //如果数值前有空格，空格会自动去除
```
- parseInt的参数不是字符转会先将参数转化为字符串，然后进行转换
```js
  parseInt(1.23) //1
  parseInt('1.23') //1
```
- 字符串转化为正数是时，试将字符逐个转换，如果遇到不能转化为数字的字符，停止转化余下字符;如果第一个字符不能转换为数字，返回NaN
```js
  parseInt('8a') //8
  parseInt('8a55') //8
  parseInt（'a123'） //NaN
```
- 如果字符串以0x或0X开头则进行十六进制进行解析，以0开头进行十进制解析，对于自动转换为科学计数法的数字，parseInt会将科学技术法作为字符串
```js
  parseInt('0x10') //16
  parseInt('011') //11
  parseInt(1000000000000000000000.5) // 1
  //等于
  parseInt（'1e+21'） //1
```
- parseInt()可以接受第二个参数（2-36），第二个参数用来表示解析值的进制，默认情况下返回的是十进制，如果第二个参数是0，null，undefined，直接忽略第二个参数
```js
  parseInt('1000',2) //8
  parseInt('10',0) //10
  parseInt('10',null) //10
  parseInt('10',undefined) //10
```
- 如果第一个参数不是字符串，先将其转换为字符串，同时也会出现一些意外的情况
```js
  parseInt(0x11,36) //43
  /*相当于*/
  parseInt(String(ox11),36);
  parseInt('17',36)
```
#### 5.2parseFloat()
- parseFloat将字符串转化为浮点数,如果字符串符合科学计数法，则进行相应转化
```js
  parseFloat('3.14') //3.14
  parseFloat('314e-2') //3.14
```
- 如果字符串中含有不能转化为浮点数的字符，不在进行下一步转换
```js
  parseFloat('3.14more non-digit characters') // 3.14
```
- parseFloat会自动过滤字符串前导空格
```js
  parseFloat('\t\v\r12.34\n') //12.34
```
- 如果参数不是字符串，或者字符串的第一个字符不能转换为浮点数，则返回NaN
```js
  parseFloat([]) //NaN
  parseFloat(''FF2) //NaN
  ParseFloat('') //NaN
```
## 字符串
### 1.概述
- 字符串是零个或多个排在一起的字符，放在单引号或双引号之中
- 单引号字符内部可以使用双引号，双引号字符内部可以使用单引号
- 如果想在单引号和双引号内部使用相同的符号，必须在内部的引号内加上反斜杠用来转义
```js
 'Did she say \'Hello\'?'
 "Did she say \"Hello\"?"
```
- 字符串默认智能在一行，在多行会报错,如果分成多行必须在每一行尾部使用反斜杠,或者使用加好链接
```js
  'a
b
c' //SyntaxError: Unexpected token ILLEGAL
  'a\
b\
c' //"abc"
 'a' +
 'b' +
 'c' //"abc"
```
- 反斜杠（‘\’）在字符中有特殊的意义
```js
  console.log('1\n2')
  //1
  //2
```
#### 字符串与数组
- 字符串可以被视为字符数组，可以利用数组的方括号来运算
- 如果方括号里面的数字超过了字符串的长度，或根本不是数字，返回undefined
```js
  var s = 'Hello';
  s[0] //"H"
  'Hello'[1] //"e"
  s[5] //undefined
  s[a] //undefined
```
- 字符串与数组的相似性仅仅是上面的，无法改变自妇产之中的字符
```js
  var s = 'Hello';
  delete s[0] //"Hello"
  s[1] = 'a' //'Hello'
```
- 字符串无法直接使用数组的方法，必须通过call方法来简介使用
```js
  var s = 'Hello';
  s.join(' ') //TypeError: s.join is not a function
  Array.protitype.join.call(s,' ') //'H e l l o'
```
#### length属性
- length属性返回字符串长度，该属性无法改变
```js
  var s = 'Hello'
  s.length //5
  s.length = 3;
  s.length //5
```
## 对象
### 1.概述
#### 1.1生成方法
- 对象是一种无序数据集合，由若干个“键值对”构成
```js
  var o = {
    p: 'Hello World',
    q: 'Hi'
  };
```
- 生成对象的三种方法
```js
  var o1 = {};
  var o2 = new Object();
  var o3 = Object.create(Object.prototype);
```
#### 1.2键名
- 对象所有的键名都是字符串，加不加引号都行
```js
  var o = {
   'p': 'Hello World !'
  }
```
- 如果键名是数值，会被自动转换为字符串
```js
 var o ={
   1: 'a',
   3.2: 'b',
   1e2: true,
   1e-2: true,
   .234: true,
   0xFF: true
 };

 o
 // Object {
 //   1: "a",
 //   3.2: "b",
 //   100: true,
 //   0.01: true,
 //   0.234: true,
 //   255: true
 // }
```
- 如果键名不符合表示名条件（第一个字符为数字，或含有空格和运算符），也不是数字，必须加上引号，否则报错
```js
  var o = {
    '1a': 'Hello',
    '1  a': 'Hello',
    '!+a': 'Hello'
  };
```
- JavaScript的保留字不可以当做键名（class，for，if..）
#### 1.3属性
- 对象的每一个键名又称为属性（property），他的键值可以是任何数据类型，如果一个属性的值为函数，通常把这个属性成为方法
```js
  var o = {
    p: function(x){
       return x*x;
    }
  }
  o.p(2) //4
```
- 属性可以动态创建，不必在对象声明是指定
```js
  var o = {};
  o.p = 123;
  o.p //123
```
#### 1.4对象的引用
- 不同的变量名指向同一个对象，那么他们都是对这个对象的引用，指向同一个内存地址，修改其中一个对象的变量，会影响其他所有变量
```js
  var o1 = {};
  var o2 = o1;
  o1.a = 1;
  o2.a //1
  o2.b = 11;
  o1.b //11
```
- 如果取消一个对象对原变量的引用，不会影响到两一个变量
```js
  var o1 = {};
  var o2 = o1;
  o1 = 1;
  o2 //{}
```
- 上面的引用方式仅限于对象，对于原始类型的数值是传值引用（拷贝）
```js
   var x = 1;
   var y = x;
   x = 2;
   y //1
```
#### 1.5表达式or语句
- 对象采用大括号表示，导致了一个问题：它是表达式or语句
```js
  {a: 123}
```
> 第一种：表示一个包含a属性的对象<br>
> 第二种: 表示一个语句，表示一个代码区块，里面有一个标签a，指向表达式123
- 为了避免歧义，JavaScript规定，如果行首为大括号，一律解释为语句，如果想表达呈对象，必须加上原括号
```js
  ({a: 123})
```
- 使用eval()语句两者差更显著
```js
  eval('{a: 123}') //123
  eval('({a: 123})') //{a: 123}
```
### 2.属性的操作
#### 2.1读取属性
- 读取对象的有两种方法：一种使用点运算符，另一种使用方括号运算符
```js
  var o = {
    p : 'Hello World'
  };
  o.p //"Hello World"
  o['p'] //"Hello World"
```
- 如果使用方括号运算符，键名必须在引号里面，否则会作为变量处理，数字键可以不加引号，数值会被当做字符串处理
- 数字键名不可以使用点运算符，只能使用方括号运算符
```js
   var o = {
     0.7: 'Hello'
   };
   o.0.7  //Uncaught SyntaxError: Unexpected number
   o['0.7'] //"Hello"
   o[0.7] //"Hello"
```
#### 2.2检查变量是否声明
- 如果读取一个不存在的键，会返回undefined，利用这一点可以来检查一个全局是否被声明
```js
   /*检查变量a是否被声明*/
   if(a) {...} //报错
   if（window.a）{...} //报错
   if (window['a']) {...} //报错
```
- 上面后两种写法之所以不会报错，是因为全局变量都是window的属性，window.a就是读取window对象的a属性，后两种也会有漏洞，如果a的是一个空的字符串或对应的布尔值为false时，则无法起到检查变量是否声明的作用，正确的写法如下
```js
  if('a' in window){
    //...
  }else {
    //...
  }
```
#### 2.3属性的赋值
- 点运算符和方括号，不仅可以用来读取数值，还可以用来赋值
```js
  var o = {};
  o.p = 1;
  o.p // 1
  o['p'] = 2;
  o.p //2
```
- JavaScript允许属性的"后绑定"，也就是说可以在任何时候增加新属性
```js
  var o = {p:1};
  /*等价于*/
  var o = {};
  o.p = 1;
```
#### 2.4查看所有的属性
- JavaScript使用Object.keys检查对象本省的所有属性
```js
  var o = {
    key1 : 1,
    key2 : 2
  }
  Object.keys(o);
  //['key1',['key2']]
```
#### 2.5delete命令
- delete用于删除对象的属性，删除成功后返回true
```js
  var o = {p:1};
  Object.keys(0)
  //['p']
  delete o.p;
  o.p //undifined
  Object.keys(0)
  //[]
```
- 删除一个不存在的属性，delete不会报错，而是返回true
```js
  var o = {};
  delete o.p  //true
```
- 有一种情况，delete命令会返回false，那就是该属性存在且不得删除
```js
  var o = Object.defineProperty({},'p'{
      value: 123,
      configurable: false
  });
  o.p //123
  delete o.p //false
```
- delete只能删除对象本身的属性，无法删除继承属性
#### 2.6in运算符
- in运算符用于检查对象是否包含某个属性
```js
  var o = {
    p: 1
  }
  'p' in o //true
```
-在JavaScript中，所有全局变量都是顶层对象window的属性，可以利用in运算符来判断一个全局变量是否存在
```js
  if('x' in window) {
    console.log('该对象存在')；
  }
```
- in运算符不能识别对象继承的属性,但对继承实行返回true
```js
  var o = new Object();
  o.hasOwnProperty('toString'); //false
  'toString' in o //true
```
#### 2.7for...in循环
- for...in循环用来便利一个对象的全部属性
```js
  var o = {a:1,b:2,c:3};
  for(var i in o){
    console.log(0[i]);
  }
  //1
  //2
  //3
```
- 使用for...in提取对象属性
```js
  var obj = {x:1,y:2};
  var props = [];
  var i = 0;
  for(props in obj);
  props //['x','y']
```
- for...in循环有两个使用注意点：(待续)
> 他遍历的对象是可以遍历（enumerable）的属性，跳过不可以遍历的属性<br>
> 他不仅可以遍历对象自身的属性，还可以遍历继承的属性
  
### 3.with语句
- with语句格式如下
 ```js
   with(object){
      statements;
   }
 ```
 - with语句是操作同一个对象多个属性时，提供更舒适的写法
 ```js
   var o = {p1:66,p2:88}; 
   with(o) {
     p1 = 1;
     p2 = 2;
   }
   /*等同于*/
   o.p1 = 1;
   o.p2 = 2;
 ```
 - 需要注意的是，with区块内部的变量，必须是当前变量已经存在的属性，否则会创建一个当前作用域的全局变量，这是因为with区块没有改变作用域，他的内部依然是当前作用域

## 数组
- 数组是按次序排列的一组值，每个位置都有编号（从0开始），整个数组用方括号包住
```js
  var a = ['a','b','c'];
  a[0] //"a"
```
- 除了定义赋值，也可以先定义后赋值
```js
  var a = [];
  a[0] = 1;
  a[1] = 2;
  a //[1,2];
```
- 任何数据都可以放入数组
```js
  var a = [
    {a:1},
    [1,2,3],
    function() {return true;}
  ]
```
- 数组的本质是一种特殊的对象
```js
  var a = [];
  typeof a //"Object"
```
- 数组的特殊性体现在，她的键名是按次序排列的一组正数(0,1,2,3...)
```js
   var a = ['a','b','c'];
   Object.keys(a);
   //['0','1','2']
```
- 对象的键名一律为字符串，数组的键名其实也是字符串，之所以可以用数值读取，是因为非字符串的键名会转化为字符串
-  在赋值时，上面的一条也是成立的，如果一个值可以转换为整数，则以该值为键名，等于对应的整数为键名
```js
  var a = [];
  a['1000'] = 1;
  a[1000] //1
  
  a[1.00] = 22;
  a[1] //22
```
- 对象有两种取值方式：一种为点结构（Object.key），另一种为方括号结构（Object[key]），数字键名不能用点结构,因为单独的数值不能作为表示符
```js
  var arr = [1,2,3];
  arr.0 //Uncaught SyntaxError: Unexpected number
```
#### length属性
```js
  [1,2,3].length //3
```
- JavaScript使用的一个32位数的整数，保存数组元素的个数，这意味着，数组成员最多有4294967295（2^32-1）个，也就是说length的最大长度为4294967295
- 只要是数组，就一定有length属性，该属性是一个动态的值，等于键名中的最大整数加1
```js
  var arr = [1,2];
  arr.length //2
  arr[2] = 3;
  arr.length //3
  arr[999] = 1000;
  arr.length //1000
```
- length的属性是可写的，如果认为设置一个小于当前成员的值，该数组的成员会自动减少到length设置的值
```js
   var a = ['a','b','c'];
   a.length //3
   a.length = 1;
   a //['a']
   a.length = 0; //将数组清空
   a //[] 
```
- 如果设置大于当前length的整数，读取新增的位置是会返回undefined
- 如果认为设置不合法的值会报错
```js
   var a = ['a','b','c'];
   a.length //3
   a.length = 5;
   a[4] //undefined
   a.length = -1; //Uncaught RangeError: Invalid array length
```
- 指的注意的是，数组本质上是对象的一种，所以我们可以给数组增加属性，但这并不影响数组length的值
```js
  var a = [];
  a['p'] = 123;
  a //[p:123]
  a.lenght //0
  a[2.11] = 'abc';
  a //[p:123,2.11:"abc"]
```
- 如果数组键名是添加超出范围的数值，该键名会自动转换为字符串
```js
  var arr = [];
  arr[-1] = 'a';
  arr[Math.pow(2,32)] = 'b';
  arr.length //0
  a //[-1:"a", 4294967296: "b"];
```
#### 类似数组的对象
- 在JavaScript中，有些对象被称为“类似数组的对象”（Array-like Object），意思是看上去很像数组，可以使用length属性，但它并不是数组，也不可以使用数组的方法
```js
  var obj = {
     0: 'a',
     1: 'b',
     2: 'c',
     length: 3
  }
  obj[0] //"a"
  obj.length  //3
  obj.push('d')  //TypeError: obj.push is not a function
```
#### in运算符在数组中的使用
- 检查键名是否存在的你运算符，适用于对象和数组
```js
  var arr = [1,2,3];
  2 in a //true
  '2' in a //true
  4 in a //false
```
- 如果数组某个位置是空位，in运算符返回false
```js
  var a = [];
  arr[100] = 'a';
  100 in a //true
  1 in a //false
```
#### for...in循环和数组的遍历
- for...in循环不仅仅可以遍历对象，也可以遍历数组，数组也是特殊的对象
```js
  var a = [1,2,3];
  for(var i in a){
     console.log(a[i])
  }
  //1
  //2
  //3
```
- for...in不仅可以遍历所有数字键，也可以遍历非数字键
```js
  var a = [1,2,3];
  a.foo = 123;
  for(var key in a){
     console.log(key)
  }
  //0
  //1
  //2
  //foo
```
#### 数组的空位
- 当数组某个位置为空元素时，既两个都好之间没有任何值，我们称概述组存在空位
- 数组的空位不影响数组的属性length
- 数组的空位是可以读取的
```js
  var a = [1,,3];
  a.length //3
  a[1] //undefined
```
- 使用delete命令删除数组成员，会形成空位，且不会影响数组的length属性
```js
  var a = [1,2,3];
  delete a[1];
  a // [1, undefined × 1, 3]
  a.length //3
```
- 数组的某个位置是空位与某个位置是undefined是不一样的，如果是空位，使用forEach方法、for...in结构，以及Object.keys方法进行遍历时，空位都会跳过
```js
  var a = [1,,3];
  a.forEach(function (x, i) {
    console.log(i + '. ' + x);
  })
  //0.1
  //2.3
  for (var i in a) {
    console.log(i);
  }
  //0
  //2
  Object.keys(a)
  //["0","2"]
```
- 如果某个位置是undefined，遍历时就不会跳过
```js
var a = [1,undefined,3];
  a.forEach(function (x, i) {
    console.log(i + '. ' + x);
  })
  //0.1
  //2.undefined
  //2.3
  for (var i in a) {
    console.log(i);
  }
  //0
  //1
  //2
  Object.keys(a)
  //["0","1","2"]

```

## 函数
- 函数就是一段可以反复调用的代码块，函数可以接受输入参数，不同的参数会返回不同的值；
### 1.1函数的声明
#### function命令
* function命令声明的代码区块，就是一个函数，function命令后面是函数名，函数名后面的圆括号里面的参数便是参入的参数，函数体放在大括号里面
```js
  function print(s) {
    console.log('Hi'+ s);
  }
```
#### 函数表达式
* 除了用function命令声明函数，还可以采用变量赋值的写法
```js
  var print = function(s){
     console.log('Hi'+ s);
  }
```
- 上面的写法是将一个匿名函数赋值给变量，这时这个匿名函数又称为函数表达式，因为赋值语句的等号右侧只能放表达式
- 采用函数表达式声明函数时，function后面不带有函数名，如果加上函数名，该函数只在函数体内部有效，函数体外部无效
```js 
  var print = function x(){
    console.log(typeof x);
  }
  x //ReferenceError: x is not defined
  print() //function
```
- 上述代码在函数表达式中，加入了函数名x，这个x只在函数体内部可以使用，指代函数表达式本身，其他地方都不可以用；这种写法有两个优点：一可以在函数体内部调用自身，二是方便排错
### Function构造函数
- Function构造函数接受三个参数，除了最后一个参数是add函数的"函数体"，其他参数都是add函数的参数，其他参数都是add函数的参数
```js
  var add = new Function(
     'x',
     'y',
     'return x + y'
  );
  /*等同于*/
  function add(x,y){
     return x + y;
  }
```
#### 函数的重复声明
- 如果一个函数被声明多次，后面的声明会覆盖前面的声明
```js
  function f(){
    console.log(1)
  }
  f() //1
  function f(){
    console.log(2)
  }
  f() //2
```
#### 圆括号运算符，return语句和递归
- 调用函数时，要使用圆括号运算符，圆括号之中可以加入参数
```js
  function add(x,y){
    return x + y;
  }
  add(1,3) //4
```
- 函数体内部的return表示返回。JavaScript引擎遇到return语句时，就会直接返回return后面的表达式，后面即便还有语句也不会执行到，也就是说return后面的表达式，就是函数返回的值，return语句不是必须的，如果没有的话，该函数就不会返回任何值，或者说返回undefined

- 函数可以调用自身，这就是递归（recursion），斐波那契数列代码
```js
  function fib(num) {
    if(num == 0) return 0;
    if(num == 1) return 1;
    return fib(nmu - 2) + fib(num - 1)
  }
  fib(6) //8
```
#### 第一等公民
- JavaScript将函数看成一种值，与其他值（数字，字符串，布尔值..）地位相同。凡是可以使用值的地方，皆可以使用函数
- 由于函数与其他类型的地位相等，所以在JavaScript中有称函数为一等公民
```js
  function add(x,y) {
    return x + y;
  }
  /*讲一个函数赋值给一个变量*/
  var operator  = add
  /*将函数作为参数和返回值*/
  function a(op) {
    return op;
  }
  a(add(1,1)) //2
```
#### 函数名的提升
- JavaScript引擎将函数名视同变量名，所以采用function命令声明函数时，整个函数会像变量声明一样，被提升到变量头部
```js
  f();
  function f() {}
```
- 表面上，上面的代码在声明之前就调用了函数f，但实际上，由于变量提升，函数f被提升到了代码头部，也就是说，函数在被条用之前就已经声明了
- 如果使用赋值语句声明函数，JavaScript就会报错
```js
  f();
  var f = function() {};
  // TypeError: undefined is not a function
  /*上面的代码等同于*/
  var f;
  f();
  function f() {};
```
- 如果同时采用function命令和赋值语句声明同一个函数，最后总是采用赋值语句定义
```js
  var f = function() {
    console.log(1);
  }
  function f(){
    console.log(2)
  }
  f() //1
```
#### 不能再条件语句中声明函数
- 根据ECMAScript的规范，不得在非函数的代码块中声明函数，最常见的就是if和try，不合法示例
```js
  if(foo) {
    function x(){}
  }
  
  try{
    functio x(){};
  }catch(e){
    console.log(e);
  }
```
- 上面的代码分别在if和try语句中声明了两个函数，按照语言规范是不合法的，但实际上浏览器不会报错
- 由于函数名的提升所以在条件语句中声明的函数，可能是无效的，这也是非常容易出错的地方
```js
  if(false) {
    function f(){};
  }
  f(); //不会报错
```
- 要达到在条件语句中定义函数的目的，只有使用函数表达式
```js
  if(false) {
    var f = function(){};
  }
  f(); //undefined
```
### 2.函数的属性和方法
#### 2.1name属性
- name属性返回紧跟在function关键字之后的那个函数名
```js
  function f1() {};
  f1.name //'f1'
  
  var f2 = function(){};
  f2.name //''
  
  var f3 = function loop() {};
  f3.name //'loop'
```
#### 2.2length的属性
- length属性返回函数预期传入参数的个数，即函数定义之中的参数个数
```js
  function add(a,b){
    return a+b
  }
  add.length //2
```
- 上面的代码定义了函数add，它的length属性就是定义时的参数个数，不管调用时输入多少个参数，length的属性始终是2
- length提供一种机制，判断定义时调用时参数的差异，以便实现面向对象编程的"方法重载"

#### 2.3toString()
- 函数toString()返回函数的源代码
```js
  function f(){
    a();
    b();
    c();
  }
  f.toString()
  //function f(){
  //  a();
  //  b();
  //  c();
  //}
```
- 函数内部注释也可以返回
```js
  function f() {/*
    这是一个
    多行注释
  */}

  f.toString()
  // "function f(){/*
  //   这是一个
  //   多行注释
  // */}"
```
- 利用这一点可以变相实现多行字符串
```js
  var multiline = function(fn){
    var arr = fn.toString().split('\n');
    return arr.slice(1,arr.length - 1).join('\n');
  };
  
  function f(){/*
      这是一个
      多行注释
  */}
  multiline(f)
  //"这是一个
  //多行注释"
```

### 3.函数的定义域
#### 3.1定义
- 作用域是指变量存在的范围。JavaScript有两种作用域：一种是全局作用域，变量在整个程序中一直存在，所有地方可以读取，另一种是函数作用域，变量只在函数内部存在
- 在函数外部声明的变量就是全局变量（globa variable）；它可以在函数内部读取
```js
  var a = 1;
  function f(){
    console.log(a);
  }
  f() //1
```
- 在函数内部定义的变量，外部无法读取，成为局部变量（local variable）
```js
  function f(){
    var a = 1;
  }
  a //ReferenceError: v is not defined
```
- 函数内部定义的变量，会在该作用域内覆盖同名的全局变量
```js
  var a = 1;
  function f(){
    var a = 2;
    console.log(a);
  }
  f() //2
  a //1
```
- 对于var命令，局部变量只能在函数内部声明，其他区块声明的，一律为全局变量
```js
  if(true) {
    var a = 5;
  }
  console.log(a); //5
```
#### 3.2函数内部的变量提升
- 与全局作用域一样，函数作用域也会产生"变量提升"的现象，var命令声明的变量，不管在什么位置，变量声明会被提升到函数体的头部
```js
  function foo(x){
    if(x > 100){
      var tmp = x -100;
    }
  }
  /*等同于*/
  function foo(x){
   var tmp;
   if(x > 100) {
     tmp = x - 100;
   }
  }
```
#### 3.3函数本身的作用域
- 函数本身也是一个值，也有自己的作用域，它的作用域与变量一样，就是生命所在的作用域，与其运行时所在的作用域无关
```js
  var a = 1;
  var x = function(){
    console.log(a);
  }
  
  function f(){
    var a = 2;
    x();
  }
  
  f() //1
```
- 函数执行时所在的作用域是定义时的作用域，而不是调用时所在的作用域
- 函数体内部声明的函数，作用域绑定函数内部
```js
  function foo(){
    var x = 1;
    function bar(){
      console.log(x);
    }
    return bar;
  }
  var x = 2;
  var f = foo();
  f() //1
```
### 参数
#### 4.1概述
- 函数运行时，有时候需要外部提供数据，这种外部数据成为参数
```js
  function square(x) {
    return x*x;
  }
  square(66) //36
```

#### 4.2参数的省略
- 函数的参数不是必须的，JavaScript允许省略参数
```js
  function(a,b){
    return a;
  }
  f(1,2,3) //1
  f(1) //1
  f() //undefined
  f.length //2
```
- 被省略的参数就会变成undefined，需要注意的是函数的length属性与实际传入的参数个数无关，只会反映函数预期传入的参数个数
- 特殊情况：没有办法只省略靠前的参数，而保留靠后的参数，如果一定要省略靠前的参数，只有显示传入undefined
```js
  function f(a,b){
    return a;
  }
  f(,2) // SyntaxError: Unexpected token ,(…)
  f(undefined, 1) // undefined
```
#### 4.3默认值
```js
  function f(a){
    a = a || 1;
    return a;
  }
  f('') //1
  f(0) //1
  f(3) //3
```
- 上面的写法会对a进行一次不二运算，只有为true时才会返回a，可是除了undefined以外，0、空字符串，null等值的布尔值也是false，也就是说，在上面的函数中，不能让a等于0或空字符串，否则在有参数的情况下，也会返回默认值
- 为了避免上面的问题，使用下面的办法来解决
```js
  function f(a) {
     (a !== undefined && a !== null) ? a = a : a = 1;
     return a;
  ]
  f() //1
  f('') //""
  f(0) //0
```
#### 4.4传递方式
- 函数的参数如果是原始值（数值，字符串，布尔值），传递方式是传值传递（passes by value），这意味着，在函数体内修改参数的值，不会影响到函数外部
```js
  var p = 2;
  functio f(p) {
    p = 3;
  }
  f(p);
  p //3
```
- 如果函数的参数是复合型的值（数组、对象、其他函数），传递方式是传址传递（pass by reference）。也就是说，传入函数的原始值的地址，在函数内部修改函数的参数值，会影响到原始值
```js
  var a = [1,2,3];
  function f(e){
    e[1] = 99;
  }
  f(a);
  a // [1,99,3]
```
- 如果函数内部修改的不是参数对象的某个属性，而是替换掉整个参数，这是并不会影响到原始值
```js
  var arr = [1,2,3];
  function f(e){
    e = [2,3,4];
  }
  f(arr);
  arr //[1,2,3]
```
- 上面的arr之所以不会受到影响，是因为形式参数e与实践参数arr存在赋值关系
```js
  /*函数内部*/
  e = arr
```
- 上面的代码，对e的修改都会反映到arr的身上，但是对e赋予一个新值，就等于切断了e与arr的联系
- 在某些特殊的情况下，也可以对原始变量进行修改，达到传址传递的效果，可以将原始值写成全局对象的属性
```js
  var a = 1;
  function f(p){
    window[p] = 2;
  }
  f('a');
  a //2
```
#### 4.5同名参数
- 如果有同名参数，则取最后出现的那个值
```js
  function f(a,a){
    console.log(a);
  }
  f(1,7) //7
```
- 如果后面没值或被省略，也是以第二个为准
```js
  function f(a,a){
    console.log(a);
  }
  f(1) //undefined
```
- 调用f函数的时候，没有第二个参数，a的取值就变成了undefined，如果这时要获取第一个参数的值，可以使用arguments对象获取
```js
   function f(){
     console.log(arguments[0])
   }
   f(1) //1
```
#### 4.6arguments对象
- 由于JavaScript允许有不定数目的参数，所以我们需要采取一定机制来读取所有参数，这便是arguments
- arguments对象包含了函数运行时的所有参数，arguments[0]就是第一个参数，arguments[1]就是第二个参数，以此类推，这个对象只有在函数体
```js
  var f = function(one){
    console.log(arguments[0]);
    console.log(arguments[1]);
    console.log(arguments[2]);
  }
  f(1,2,3)
  //1
  //2
  //3
```
- arguments除了读取参数，汉可以为参数赋值（严格模式下不允许这中做法）
```js
  var f = function(a,b){
    arguments[0] = 11;
    arguments[1] = 22;
    return a + b;
  }
  f(1,1) //33
```
- 通过arguments对象的属性，可以判断调用时到底带了几个参数
```js
  function f(){
    return arguments.length
  }
  f(1,2,3) //3
  f() //0
```
### 5.函数的其他知识点
#### 5.1闭包
- 闭包是JavaScript语言的一个难点，也是它的特色；要了解闭包，首先必须理解变量的作用域，理解全局变量和局部变量
- 出于种种原因，我们需要得到函数内部的局部变量，正常情况下是办不到的，只有变通方法才能获取，那就是在函数内部再次定义一个函数
```js
  function f1(){
    var n = 999;
    function f2(){
      console.log(n)
    }
    return f2;
  }
  var result = f1();
  result(); //999
```
- 上面的代码中函数f1返回了函数f2的值，由于f2可以读取f1的内部变量，所以就可以在外部获取f1的内部变量
- 闭包可以简单的理解为定义在一个函数内部的函数，闭包的最大特点就是可以记住他的诞生环境，本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁
- 闭包的最大用处有两个：一是可以读取函数的内部变量，另一个就是让这些变量始终保存在内存中，及闭包可以使它的诞生环境一直存在
```js
  function remember(e){
    return function(){
      return e++;
    }
  }
  var add = remember(5);
  add() //5
  add() //6
  add() //7
```
#### 5.2立即调用函数表达式（IIFE）
- 在JavaScript中()是一个运算符，跟在函数名之后表示调用该函数，比如add()
- 有时我们在自定义函数之后，立即调用该函数，这是不能在之后加圆括号，这会产生语法错误
```js
  function(){...}();
  // SyntaxError: Unexpected token (
```
- 上面代码的错误原因是，function这个关键字既可以当做语句，也可以作为表达式
```js
  //语句
  function f(){}
  //表达式
  var f = function f() {}
```
- 为了避免解析上的歧义，JavaScript引擎规定，如果function关键字出现在行首，一律解释为语句，JavaScript引擎看到行首是function关键字之后，认为这一段是函数定义，不该以圆括号结尾，所以报错
- 解决办法就是不让function出现在行首，让引擎将其理解呈一个表达式，最简单的就是，将其放在一个圆括号内
```js
  (function(){....}());
  //or
  (function(){})();
```
- 上面两种写法最后面的分后都是必须的，如果省略分号连着写两个IIFE函数，可能会报错
```js
   // 报错
  (function(){ /* code */ }())
  (function(){ /* code */ }())
```
- 上面两行代码没有分号，JavaScript会将它们连载一起解释，将第二行解释为第一行的参数

### 6.eval命令
- eval命令的作用是将字符串当做语句来执行
```js
  eval('var a = 1');
  a //1
```
- 放在eval中的字符串应该有独自存在的意义，不能用来与eval以外的命令配合使用
```js
  eval('return;')
  //Uncaught SyntaxError: Illegal return statement
```
- eval没有自己的作用域，都在当前作用域执行，因此可能会修改当前作用域变量的值，造成安全问题
```js
  var a = 1;
  eval('a = 2');
  a //2
```


## 运算符
### 1.加法运算符
- 加法运算符是最常见的运算符之一，加法运算符有两种运算模式：处理算术的加法，也可以用作字符串链接
```js
  //加法
  1 + 1 //2
  true + true //2
  1 + true //2
  
  //字符串链接
  '1' + '1' //"11"
  '1.1' + '1.1' //"1.11.1"
```
- 加法的算法步骤如下




