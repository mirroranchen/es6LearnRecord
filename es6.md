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