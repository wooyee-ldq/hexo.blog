---
title: javaScript变量声明方式
date: 2019-06-10 23:27:53
tags: javaScript
---

## javaScript声明变量，可以通过let、var、const来声明：

* #### let：块级变量声明【***es6新增的声明变量方式*** 】

  * ##### 作用域是块级作用域

    ```bash
    if(true){
    	let a = 1;
    	console.log(a);
    }
    ```

  * ##### 不存在变量提升

    ```bash
    console.log(a); //这里会报错：ReferenceError: a is not defined
    let a = 1;
    ```

  *  ##### 不能重复定义

    ```bash
    let a = 1;
    let a =2; //这里会报错：SyntaxError: Identifier 'a' has already been declared
    ```

  * ##### 存在暂时性死区

    ```bash
    let a = 1;
    if(1){
       console.log(a);  //这里会报错：ReferenceError: a is not defined,去掉这语句后，输出a结果为：2
        let a = 2;
        console.log(a);
    }
    ```

- #### var 【es6前 就用来声明变量的方法】

  * ##### var的作用域是函数作用域，在一个函数内利用var声明一个变量，则这个变量只在这个函数内有效

    ```bash
    function test(){
     var a = 1;
    console.log(a);
    }
    test(); // 输出结果：1
    console.log(a); //这里会报错：ReferenceError: a is not defined
    ```

  * ##### 存在变量提升

    ```bash
    console.log(test);
    var test = 1;
    //不会报错，结果为：undefined
    ```

* #### const一般用来声明常量，且声明的常量是不允许改变的，只读属性，因此就要在声明的同时赋值。

  * ##### const与let一样，都是块级作用域，存在暂时性死区，不存在变量提升，不允许重复定义

  * ##### 声明的常量是不允许改变

    ```bash
    const a = 1;
    a = 2; //这里会报错：TypeError: Assignment to constant variable.
    ```

---

> > ***到此，javaScript三种变量声明就介绍完了......***

