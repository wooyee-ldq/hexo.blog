---
title: ECMAScript基础之预编译【变量提升】
date: 2019-06-07 21:43:28
tags: javaScript
---

## ***javaScript包括ECMAScript、DOM和BOM，ECMAScript就是javaScript的最基础语法。这里将介绍ECMAScript的基础内容：预编译***【变量提升】

#### 预编译有两种情况，一种是整个文档在运行之前发生的预编译，还有就是函数在执行前发生的预编译。

---

#### *开始预编译：*

##### ***文档代码执行前：***

```bash
{
	1.创建GO对象(global object)
	2.找变量声明，将变量名作为GO对象的属性名，此时值为undefined
	3.找函数声明，把函数名作为GO对象的属性名，把函数体作为值赋给对应的属性名
	4.开始执行代码，当执行到函数的时候，要在函数执行前进行预编译
}
```

##### ***函数执行前：***

```bash
{
	1.创建AO对象（执行期上下文 activation object）
	2.找函数形参和变量声明，将形参名和变量名作为AO对象的属性名，此时值为undefined
	3.将实参值和形参值统一
	4.在函数体里找函数声明，把函数名作为AO对象的属性名，把函数体作为值赋给对应的属性名
}
```

#### ***这里举个栗子，看下面代码的预编译过程：***

```javascript
console.log(a);
var a = 1;
console.log(b);
function b(num1, num2){
    console.log(num1);
    var t = num1;
    num1 = num1 + num2;
    function num1(){}
    console.log(num1);
    num2 = t - num2;
    return num2;
}
b(a,2);
```

#### 运行结果：

```bash
undefined
[Function: b]
[Function: num1]
function num1(){}2
```

#### 预编译过程：

```bash
#1.创建GO对象(global object)
GO{
	
}
#2.找变量声明，将变量名作为GO对象的属性名，此时值为undefined
GO{
	a: underfined,
}
#3.找函数声明，把函数名作为GO对象的属性名，把函数体作为值赋给对应的属性名
GO{
	a: underfined,
	b: function(num1, num2){...},
}
#4.开始执行代码，当执行到函数的时候，要在函数执行前进行预编译:
> console.log(a)
< underfined
> a = 1
< 1	#此时GO中a的值变为：1
> console.log(b)
< [Function: b]
> b(a,2)
< #这里执行前要进行预编译：
#1.创建AO对象（执行期上下文 activation object）
AO{

}
#2.找函数形参和变量声明，将形参名和变量名作为AO对象的属性名，此时值为undefined
AO{
	num1: underfined,
	num2: underfined,
	t: underfined,
}
#3.将实参值和形参值统一
AO{
	num1: 1,
	num2: 2,
	t: underfined,
}
#4.在函数体里找函数声明，把函数名作为AO对象的属性名，把函数体作为值赋给对应的属性名
AO{
	num1: function(){},
	num2: 2,
	t: underfined,
}
#继续运行：
> console.log(num1)
< [Function: num1]
> t = num1
< function(){}
> num1 = num1 + num2	#此时AO中的num1变为：function num1(){}2
> console.log(num1)
< function num1(){}2
> ...
```

#### 所以输出的结果是：

```bash
undefined
[Function: b]
[Function: num1]
function num1(){}2
```

---

> > ***到此，预编译就介绍完了......***

