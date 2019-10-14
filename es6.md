### 1.let 与 const

#### 1.1 let

声明的变量只在let命令所在的代码块内有效。

````
{
    let a = 0;
}
a // 
````

![1571039316974](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1571039316974.png)

##### 1.1.1 代码块内有效

let 是在代码块内有效，var 是在全局里有效

````
{
    let a = 0;
    var b = 1;
}
````

> 注：由于a报错，一个一个打印。

打印结果a not defined ；b=1

##### 1.1.2 不能重复声明

let 只能声明一次，var可以声明多次

````
let a = 1;
let a = 2;
var b = 3;
var b = 4;
a  // Identifier 'a' has already been declared
b  // 4
````

##### 1.1.3 for 循环 

````
for (var i = 0; i < 10; i++) {
  setTimeout(function(){
    console.log(i);
  })
}
// 输出十个 10
for (let j = 0; j < 10; j++) {
  setTimeout(function(){
    console.log(j);
  })
}
// 输出 0123456789
````

var 在全局有效，let在循环体有效

##### 1.1.4 不存在变量提升

let不存在变量提升，var会变量提升

````
console.log(a);  //ReferenceError: a is not defined
let a = "apple";
 
console.log(b);  //undefined
var b = "banana";
````

#### 1.2const 命令

const 声明一个只读变量，声明之后不允许改变。意味着，一旦声明必须初始化，否则会报错。

````
const a = 100;
console.log(a)
const b;

````

![1571042850477](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1571042850477.png)

### 2 ES6解构赋值

概述

解构赋值是对赋值运算符的扩展

他是一种针对数组或者对象进行模式匹配，然后对其中的变量进行赋值。

在代码书写上简洁且易读，语义更加清晰明了；也方便了复杂对象中数据字段获取。

#### 2.1 数组模型的解构（Array）

##### 2.1.1 基本

````
let [a, b, c] = [1, 2, 3]
//a = 1;b = 2;c = 3;
````

##### 2.1.2可嵌套

````
let [a, [b], c]=[1, [2], 3]
//a = 1;b = 2;c = 3;
````

##### 2.1.3 可忽略

````
let [a, , b] = [1, 2, 3];
//a = 1;c = 3;
````

#####　2.1.４不完全解构

````
let [a = 1,b]=[];
// a = 1,b = undefined
````

##### 2.1.5 剩余运算符

````
let [a, ...b] = [1,2,3]
````

##### 2.1.6 字符串等

在数组的解构中，解构的目标若为可遍历对象，皆可进行解构赋值。可遍历对象即实现 Iterator 接口的数据。

````
let [a, b, c, d, e] = 'hello';
````

