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
  for(var i=0;i<3:i++){
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
```















