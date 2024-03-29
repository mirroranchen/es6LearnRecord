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
//a = 1; b = 2; c = 3;
````

##### 2.1.2可嵌套

````
let [a, [b], c]=[1, [2], 3]
//a = 1; b = 2; c = 3;
````

##### 2.1.3 可忽略

````
let [a, , b] = [1, 2, 3];
//a = 1; c = 3;
````

#####　2.1.４不完全解构

````
let [a = 1,b]=[];
// a = 1, b = undefined
````

##### 2.1.5 剩余运算符

````
let [a, ...b] = [1,2,3]
// a = 1, b = [2, 3]
````

##### 2.1.6 字符串等

在数组的解构中，解构的目标若为可遍历对象，皆可进行解构赋值。可遍历对象即实现 Iterator 接口的数据。

```` 
let [a, b, c, d, e] = 'hello';
//a = 'h', b = 'e', c = 'l', d = 'l', e = 'o'
````

##### 2.1.7 解构默认值

````
let [a = 1] = [undefined]; // a = 1
````

当解构模式有匹配结果，且匹配结果是 undefined 时，会触发默认值作为返回结果。

````
let [a = 3, b = a] = [];     // a = 3, b = 3
let [a = 3, b = a] = [1];    // a = 1, b = 1
let [a = 3, b = a] = [1, 2]; // a = 1, b = 2
````

- a 与 b 匹配结果为 undefined ，触发默认值：a = 3; b = a =3
- a 正常解构赋值，匹配结果：a = 1，b 匹配结果 undefined ，触发默认值：b = a =1
- a 与 b 正常解构赋值，匹配结果：a = 1，b = 2;

#### 2.2对象模型的解构(Object)

##### 2.2.1 基本

````
let { anne , lister} = { anne : 'love', lister : 'ann' }
// anne = 'love', lister = 'ann'
````

```
let { anne : ann} = { anne : 'mariana'}
// ann = 'mariana'
```

##### 2.2.2 可嵌套可忽略

````
let obj = {p: ['hello', {y: 'world'}]};
let {p: [x,{y}]} = obj;
// x = 'hello'
// y = 'world'
let obj = {p: ['hello', {y: 'world'}] };
let {p: [x, {  }] } = obj;
// x = 'hello'
````

##### 2.2.3 不完全解构

````
let obj = {p: [{y: 'world'}] };
let {p: [{ y }, x ] } = obj;
// x = undefined
// y = 'world'
````

##### 2.2.4 剩余运算符

````
let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40};
// a = 10
// b = 20
// rest = {c: 30, d: 40}
````

##### 2.2.5 解构默认值

````
let {a = 10, b = 5} = {a: 3};
// a = 3; b = 5;
let {a: aa = 10, b: bb = 5} = {a: 3};
// aa = 3; bb = 5;
````

### 3 Es6 Symbol

#### 3.1 概述

ES6 引入了一种新的原始数据类型 Symbol ，**表示独一无二的值，最大的用法是*用来定义对象的唯一属性名***。

ES6 数据类型除了 Number 、 String 、 Boolean 、 Objec t、 null 和 undefined ，还新增了 Symbol 。

#### 3.2 基本用法

Symbol 函数栈不能用 new 命令，因为 Symbol 是原始数据类型，不是对象。可以接受一个字符串作为参数，为新创建的 Symbol 提供描述，用来显示在控制台或者作为字符串的时候使用，便于区分。

````
let sy = Symbol('lister');
console.log(sy) // Symbol(lister)
console.log(typeof(sy)); // symbol
// 相同参数 Symbol() 返回的值不相等
let sy1 = Symbol('lister');
console.log(sy === sy1) //false

````

#### 3.3 使用场景

##### 3.3.1 作为属性名

用法

**由于每一个 Symbol 的值都是不相等的，所以 Symbol 作为对象的属性名，可以保证属性不重名。**

````
let sy = Symbol('key1');

//写法1
let syObject = {}
syObject[sy] = 'kk'
console.log(syObject)
// {Symbol(key1): 'kk'}

//写法2
let syObject = {
    [sy]: 'kk'
}

// 写法3
let syObject = {};
Object.defineProperty(syObject, sy, {value: "kk"});
console.log(syObject);   // {Symbol(key1): "kk"}
````

Symbol 作为对象属性名时不能用.运算符，要用方括号。因为.运算符后面是字符串，所以取到的是字符串 sy 属性，而不是 Symbol 值 sy 属性

````
let sy = Symbol('key1');
let syObject = {}
syObject[sy] = 'lister'
//syObject[sy];  // "lister"
//syObject.sy;   // undefined
````

##### 3.3.2 注意点

Symbol 值作为属性名时，该属性是公有属性不是私有属性，可以在类的外部访问。但是不会出现在 for...in 、 for...of 的循环中，也不会被 Object.keys() 、 Object.getOwnPropertyNames() 返回。如果要读取到一个对象的 Symbol 属性，可以通过 Object.getOwnPropertySymbols() 和 Reflect.ownKeys() 取到。

````
let sy = Symbol('lister');
let syObject = {}
syObject[sy]='walker'
console.log(syObject)
for (let i in syObject) {
   console.log(i)
}

console.log(Object.keys(syObject)); //[]
console.log(Object.getOwnPropertySymbols(syObject))//[Symbol(lister)]
console.log(Reflect.ownKeys(syObject))
````

##### 3.3.3 定义常量

#### 3.4 Symbol.for()

Symbol.for() 类似单例模式，首先会在全局搜索被登记的 Symbol 中是否有该字符串参数作为名称的 Symbol 值，如果有即返回该 Symbol 值，若没有则新建并返回一个以该字符串参数为名称的 Symbol 值，并登记在全局环境中供搜索。

````
let yellow = Symbol("Yellow");
let yellow1 = Symbol.for("Yellow");
yellow === yellow1;      // false
 
let yellow2 = Symbol.for("Yellow");
yellow1 === yellow2;     // true
````

#### 3.5 Symbol.keyFor()

Symbol.keyFor() 返回一个已登记的 Symbol 类型值的 key ，用来检测该字符串参数作为名称的 Symbol 值是否已被登记.

````
let yellow1 = Symbol.for("Yellow");
Symbol.keyFor(yellow1);    // "Yellow"
````

### 4 Es6 字符串

ES6 之前判断字符串是否包含子串，用 indexOf 方法，ES6 新增了子串的识别方法。

#### 4.1 字符串新增

- **includes()**：返回布尔值，判断是否找到参数字符串。
- **startsWith()**：返回布尔值，判断参数字符串是否在原字符串的头部。
- **endsWith()**：返回布尔值，判断参数字符串是否在原字符串的尾部。

````
let string = "lister,walker,mariana";
string.includes("lister")
console.log(string.includes("lister"));
// true
console.log(string.startsWith("lister"));
// true
console.log(string.endsWith("walker"));
// false
console.log(string.startsWith("walker",7))
//true
````

**注意点：**

- 这三个方法只返回布尔值，如果需要知道子串的位置，还是得用 indexOf 和 lastIndexOf 。
- 这三个方法如果传入了正则表达式而不是字符串，会抛出错误。而 indexOf 和 lastIndexOf 这两个方法，它们会将正则表达式转换为字符串并搜索它。

#### 4.2 字符串重复

repeat():返回新的字符串，表示将字符串重复指定次数返回

````
console.log("Hello,".repeat(2)); 
````

如果是小数，向下取整

````
console.log("Hello".repeat(3.2))
````

如果是0到-1之间的小数，取0

````
console.log("lister,".repeat(-0.5))  ''
````

如果参数是 NaN，等同于 repeat 零次

````
console.log("Hello,".repeat(NaN)); ''
````

如果参数是负数或者 Infinity ，会报错:

````
console.log("Hello,".repeat(-1)); 
console.log("Hello,".repeat(Infinity));
````

#### 4.3 字符串补全

- **padStart**：返回新的字符串，表示用参数字符串从头部（左侧）补全原字符串。
- **padEnd**：返回新的字符串，表示用参数字符串从尾部（右侧）补全原字符串。

以上两个方法接受两个参数，第一个参数是指定生成的字符串的最小长度，第二个参数是用来补全的字符串。如果没有指定第二个参数，默认用空格填充。

````
console.log("r".padStart(6,'liste'))
console.log("l".padEnd(6,"ister"));
// lister
````

如果指定的长度小于或者等于原字符串的长度，则返回原字符串:

````
console.log('hello'.padStart(5,'a')); // hello
````

如果原字符串加上补全字符串长度大于指定长度，则截去超出位数的补全字符串:

````
console.log('lister'.padEnd(10,'walker'))
````

常用于补全位数：

````
console.log('0123'.padEnd(10,'456789'))
````

#### 4.4 模板字符串

模板字符串相当于加强版的字符串，用反引号 `,除了作为普通字符串，还可以用来定义多行字符串，还可以在字符串中加入变量和表达式。

基本用法

普通字符串

````
let shibden = `Miss'\n'lister`;
console.log(shibden)
````

多行字符串

````
let shibden = `miss lister
and miss walker`
console.log(shibden)
````

字符串插入变量和表达式。

变量名写在 ${} 中，${} 中可以放入 JavaScript 表达式

````
let name = 'lister';
let age = 40;
let info = `Shibden's host is ${name}, her age is ${age+1} years old this year`
console.log(info)
````

字符串中调用函数：

````
function f(){
    return 'love walker'
}
let info = `lister ${f()}`;
console.log(info)
````

**注意要点**

模板字符串中的换行和空格都是会被保留的

````
innerHtml = `
    <ul>
    <li>heihei</li>
    <li>hahha</li>
    </ul>
`
console.log(innerHtml)
//  <ul>
    <li>heihei</li>
    <li>hahha</li>
    </ul>
````

#### 4.5 标签模板

````
alert`Miss Lister`;
等同于alert('Miss Lister')
````

### 5 ES6对象

对象字面量

#### 5.1 属性的简洁表示法

ES6允许对象的属性直接写变量，这时候属性名是变量名，属性值是变量值。

````
const age = 41;
const name = 'lister';
const person = {age, name}
console.log(person)
//{age: 41, name: "lister"}
````

#### 5.2 方法名也可以缩写.

````
const person = {
    sayHi(){
        console.log('hi');
    }
}
person.sayHi();

````

如果是Generator函数，则要在前面加一个*

````
const obj = {
    *myGenerator() {
        yield 'hello Miss Lister'
    }
}
//等同于
const obj = {
  myGenerator: function* () {
    yield 'hello world';
  }
};
````

#### 5.3 属性名表达式

ES6允许用表达式作为属性名，但是一定要将表达式放在方括号内。

````
const obj = {
    ['li'+'ster'](){
        return 'lister love Miss Walker'
    }
}

console.log(obj.lister())
````

注意点：属性的简洁表示法和属性名表达式不能同时使用，否则会报错。

````
const hello = "Hello";
const obj = {
 [hello]
};
obj  //SyntaxError: Unexpected token }
 
const hello = "Hello";
const obj = {
 [hello+"2"]:"world"
};
obj  //{Hello2: "world"}
````

#### 5.4 对象的拓展运算符

拓展运算符（...）用于取出参数对象所有可遍历属性然后拷贝到当前对象。

基本用法

````
let person = {name:'lister', age: 41};
let somebody = { ...person}
console.log(person);
// {name: "lister", age: 41}
````

自定义的属性和拓展运算符对象里面属性的相同的时候：**自定义的属性在拓展运算符后面，则拓展运算符对象内部同名的属性将被覆盖掉。**

````
let person = {name: "Amy", age: 15};
let someone = { ...person, name: "Mike", age: 17};
someone;  //{name: "Mike", age: 17}
````

自定义的属性在拓展运算度前面，则变成设置新对象默认属性值。

````
let person = {name: "Amy", age: 15};
let someone = {name: "Mike", age: 17, ...person};
someone;  //{name: "Amy", age: 15}
````

拓展运算符后面是空对象，没有任何效果也不会报错。

````
let a = {...{}, a: 1, b: 2};
a;  //{a: 1, b: 2}
````

拓展运算符后面是null或者undefined，没有效果也不会报错

````
let b = {...null, ...undefined, a: 1, b: 2};
b;  //{a: 1, b: 2}
````

#### 5.5 对象的新方法 assign

用于将源对象的所有可枚举属性复制到目标对象中。

基本用法

```
let a = {a:1}
let b = {b:2}
Object.assign(a,b)
console.log(a)
//{a: 1, b: 2}
```

- 如果目标对象和源对象有同名属性，或者多个源对象有同名属性，则后面的属性会覆盖前面的属性。

````
let a = {a:1}
let b = {a:2}
Object.assign(a,b)
console.log(a)
//{a: 2}
// ----------------
let a = {a:1}
let b = {a:2}
let c = {a:3}
Object.assign(a,b,c)
console.log(a)
//{a: 3}
````

- 如果该函数只有一个参数，当参数为对象时，直接返回该对象；当参数不是对象时，会先将参数转为对象然后返回。

````
let a = Object.assign(3);
console.log(a)
//Number {3}
let b = typeof(Object.assign(3))
console.log(b)
//object
````

**注意点**

assign 的属性拷贝是浅拷贝:

#### 5.6 Object.is(value1, value2)

用来比较两个值是否严格相等，与（===）基本类似

基本用法

````
let a = Object.is("q","q"); 
console.log(a) //true
Object.is(1,1);          // true
Object.is([1],[1]);      // false
Object.is({q:1},{q:1});  // false
````

与（===）的区别

````
//一是+0不等于-0
Object.is(+0,-0);  //false
+0 === -0  //true
//二是NaN等于本身
Object.is(NaN,NaN); //true
NaN === NaN  //false
````

### 6 ES6 数组

#### 6.1 数组创建

##### 6.1.1 Array.of()

将参数中所有值作为元素形成数组。

````
console.log(Array.of(1,2,3,4))
//(4) [1, 2, 3, 4]

// 参数值可为不同类型
console.log(Array.of(1, '2', true)); // [1, '2', true]
 
// 参数为空时返回空数组
console.log(Array.of()); // []
````

##### 6.1.2 Array.from()

将类数组对象或可迭代对象转化为数组。

````
// 参数为数组,返回与原数组一样的数组
console.log(Array.from([1,2,3]))
//(3) [1, 2, 3]
console.log(Array.from([1, , 3])); 
// [1, undefined, 3]
````



```
Array.from(arrayLike[, mapFn[, thisArg]])
```

返回值为转换后的数组。

**arrayLike**

````
console.log(Array.from([1, 2, 3])); // [1, 2, 3]
````

mapFn

可选，map 函数，用于对每个元素进行处理，放入数组的是处理后的元素。

````
console.log(Array.from([1, 2, 3],(n)=>n*2)); 
//[2, 4, 6]
````

thisArg

可选，用于指定 map 函数执行时的 this 对象。


````
let map = {
    do: function(n) {
        return n * 2;
    }
}
let arrayLike = [1, 2, 3];
console.log(Array.from(arrayLike, function (n){
    return this.do(n);
}, map)); // [2, 4, 6]
````

##### 6.1.3 类数组对象

一个类数组对象必须含有 length 属性，且元素属性名必须是数值或者可转换为数值的字符。

````
let arr = Array.from({
    0:1,
    1:2,
    2:3,
    length:3
})
console.log(arr)
//-------------------------------
//没有length，会报错
let arr = Array.from({
    0:1,
    1:2,
    2:3,
    length:3
})
console.log(arr)
//// 元素属性名不为数值且无法转换为数值，返回长度为 length 元素值为 undefined 的数组  
let arr = Array.from({
    a:1,
    b:2,
    c:3,
    length:3
})
console.log(arr);
// [undefined, undefined, undefined]
````



##### 6.1.4 转换可迭代对象

转换map 

````
let map = new Map();
map.set('name1','lister');
map.set('name2','lister2');
console.log(Array.from(map))
//[Array(2), Array(2)]
````

**转换 set**

````
let arr = [1,2,3];
let set = new Set(arr);
console.log(Array.from(set))
//[1, 2, 3]
````

**转换字符串**

````
let str = 'lister'
console.log(Array.from(str));
// ["l", "i", "s", "t", "e", "r"]

````

####　6.2扩展的方法

##### 6.2.1 查找

find()

查找数组中符合条件的元素,若有多个符合条件的元素，则返回第一个元素。

`````
let arr = Array.of(1,2,3,4)
console.log(arr.find(item=>item>3))
//4
// 数组空位处理为 undefined
console.log([, 1].find(n => true)); // undefined
`````

findIndex()

查找数组中符合条件的元素索引，若有多个符合条件的元素，则返回第一个元素索引。

````
let arr = Array.of(1, 2, 1, 3);
// 参数1：回调函数
// 参数2(可选)：指定回调函数中的 this 值
console.log(arr.findIndex(item => item = 1)); // 0
// 数组空位处理为 undefined
console.log([, 1].findIndex(n => true)); //0
````

##### 6.2.2填充

fill()

将一定范围索引的数组元素内容填充为单个指定的值

````
let arr = Array.of(1,2,3,4)
// 参数1：用来填充的值
// 参数2：被填充的起始索引
// 参数3(可选)：被填充的结束索引，默认为数组末尾
console.log(arr.fill(10,3,4))
// [1, 2, 3, 10]
````

**copyWithin()**

将一定范围索引的数组元素修改为此数组另一指定范围索引的元素。

// 参数1：被修改的起始索引
// 参数2：被用来覆盖的数据的起始索引
// 参数3(可选)：被用来覆盖的数据的结束索引，默认为数组末尾

````
console.log([1,2,3,4,5,6].copyWithin(0,3,5))

//4,5,3,4,5,6


// 参数1为负数表示倒数
console.log([1,2,3,4,5,6].copyWithin(-2,0))

//1,2,3,4,1,2

console.log([1,2, ,4].copyWithin(0,2,4));
// [empty, 4, empty, 4]
````

##### 6.2.3遍历

 **entries()**遍历键值对。

  **keys()**遍历键名

 **values()**遍历键值。

#### 6.3 包含

includes（）数组是否包含指定值。

注意：与 Set 和 Map 的 has 方法区分；Set 的 has 方法用于查找值；Map 的 has 方法用于查找键名。

````
// 参数1：包含的指定值
console.log([1,2,3].includes(1))//true
````

####　6.4嵌套数组转一维数组

flat（）

````
console.log([1,[2,3]].flat());//[1,2,3]
// 指定转换的嵌套层数
console.log([1, [2, [3, [4, 5]]]].flat(2)); // [1, 2, 3, [4, 5]]
 
// 不管嵌套多少层
console.log([1, [2, [3, [4, 5]]]].flat(Infinity)); // [1, 2, 3, 4, 5]
 
// 自动跳过空位
console.log([1, [2, , 3]].flat());<p> // [1, 2, 3]
````

#### 6.5 扩展运算符

复制数组

````
let arr = [1,2]
let arr1 = [...arr]
console.log(arr1)
````

合并数组

````
console.log([...[1,2],...[7,8]])
//[1,2,7,8]
````

### 7 Es6函数

#### 7.1 函数参数的扩展

##### 7.1.1 默认参数

基本用法

````
function fn(name,age=41){
    console.log(name+','+age)
}
fn('lister',42)
fn('lister','')
fn('lister')
````

> 注意点：使用函数默认参数时，不允许有同名参数。

只有在未传递参数，或者参数为 undefined 时，才会使用默认参数，null 值被认为是有效的值传递。

````
function fn(name,age=41){
    console.log(name+','+age)
}
fn('lister',undefined)
//lister ,41

//----------------
function fn(name,age=41){
    console.log(name+','+age)
}
fn('lister',null)
//lister ,null
````

##### 7.1.2 不定参数

不定参数用来表示不确定参数个数，形如，...变量名，由...加上一个具名参数标识符组成。具名参数只能放在参数组的最后，并且有且只有一个不定参数。

基本用法

````
function fn(...values){
    console.log(values.length)
}
f(1,2) //2
````

#### 7.2 箭头函数

箭头函数提供了一种更加简洁的函数书写方式。基本语法是：

参数=>函数体

基本用法

````
var f = v => console.log(v);
//等价于
var f2 = function(a){
 return a;
}
f(1);  //1
````

当箭头函数没有参数或者有多个参数，要用 () 括起来

当箭头函数函数体有多行语句，用 {} 包裹起来，表示代码块，当只有一行语句，并且需要返回结果时，可以省略 {} , 结果会自动返回。

当箭头函数要返回对象的时候，为了区分于代码块，要用 () 将对象包裹起来

`````
// 报错
var f = (id,name) => {id: id, name: name};
f(6,2);  // SyntaxError: Unexpected token :
 
// 不报错
var f = (id,name) => ({id: id, name: name});
f(6,2);  // {id: 6, name: 2}
`````

注意点：没有 this、super、arguments 和 new.target 绑定。

箭头函数体中的 this 对象，是定义函数时的对象，而不是使用函数时的对象

### 8 Es6 迭代器

iterator

Iterator 是 ES6 引入的一种新的遍历机制，迭代器有两个核心概念：

+ 迭代器是一个统一的接口，它的作用是使各种数据结构可被便捷的访问，它是通过一个键为Symbol.iterator 的方法来实现。
+ 迭代器是用于遍历数据结构元素的指针（如数据库中的游标）

### 9 es6 Class类

在ES6中，class (类)作为对象的模板被引入，可以通过 class 关键字定义类。

class 的本质是 function。

它可以看作一个语法糖，让对象原型的写法更加清晰、更像面向对象编程的语法。

#### 9.1 基础用法

##### 9.1.1 类定义

类表达式可以为匿名或命名。

````
//匿名类
//类表达式可以为匿名或命名
let Example = class {
    constructor(a){
        this.a = a
    }
}
//命名类
let Example = class Example {
    constructor(a){
        this.a = a;
    }
}
````

##### 9.1.2 类声明

````
class Example {
    constructor(a){
        this.a = a;
    }
}
````

注意要点：不可重复声明。