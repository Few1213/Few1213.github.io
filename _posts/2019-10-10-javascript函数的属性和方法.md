---
layout: post
title: "javascript函数的属性和方法"
subtitle: "javascript 函数 "
author: "Few"
header-img: "img/home-bg-art.jpg"
header-mask: 0.4
tags:
  - github
  - blog
  - javascript
  - function
---



javascript函数的属性和方法

	在ECMAScript中的函数是对象,所以函数也具有属性和方法,每个函数都包含两个属性:

1.length:表示函数希望接收的命名参数的个数。

 1.  ```javascript
     function sayName(name){
         alert(name);
     	}
     ```

     ```
     function sum(num1, num2){
         return num1 + num2;
         }
     ```

     ```
     function sayHi(){
         alert("hi");
     	}
     ```

     ```
     alert(sayName.length);      //1
     alert(sum.length);          //2
     alert(sayHi.length);        //0
     ```

     以上代码定义的三个函数，每个函数接收的命名参数的个数不同，各自所返回的length属性的值也不同。



2.prototype:原型，是保存它们所有实例方法的真正所在，prototype 属性是不可枚举的，因此使用 for-in 无法发现。



两个非继承而来的方法 apply() 和 call()

1.apply(对象,[参数1,参数,参数3,....]) 

	两个参数： 一个数在其中运行函数的作用域，另一个数参数数组（第二个参数可以是 array 的实例，也可以是 arguments 对象）

```
function sum(num1, num2){
    return num1 + num2;
    }
```

```
function callSum1(num1, num2){
    return sum.apply(this, arguments);//传入 arguments 对象
	}
```

```
function callSum2(num1, num2){
    return sum.apply(this, [num1, num2]);//传入数组
    }
```

```
alert(callSum1(10,10));   //20
alert(callSum2(10,10));   //20
```

	这两个函数都会正常执行并返回正确的结果。
2.call(对象,参数1,参数2,参数3,...)

	call() 方法和 apply() 方法的作用相同，他们的区别仅在于接收参数的方式的不同。

  使用call() 或 apply() 来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系。



函数的内部属性 arguments 和 this

	1.argements: 类数组对象，包含着传入函数中的所有参数，主要用途是保存函数参数，但是有一个名叫 callee 的属性，该属性是一个指针，指向拥有这个 arguments 对象的函数。

```
 function factorial(num){
        if (num <=1) {
            return 1;
        } else {
            return num * factorial(num-1)
        }
    }
```

```

function factorial(num){
        if (num <=1) {
            return 1;
        } else {
            return num * arguments.callee(num-1)
        } 
     } 
```

	使用 arguments.callee 可以消除函数紧密耦合的现象。

	

	2.this: this 引用的是函数据以执行的环境对象---或者也可以说是 this 的值。

this的指向问题

	调用模式,this指向的是window

        对象(方法)调用模式:谁调用这个方法,this指向谁

        构造函数模式,this指向的屙屎新创建出来的实例对象

        上下文模式(借用模式)





	



	 
