# 前端面经
## JS
* JS数据类型有哪些？
```
1、基本数据类型：String、Number、Boolean、Null、Underfined、Symbol（ES6新增，表示独一无二的值）；
2、引用类型：Object。
基本数据类型在内存中是栈存储，引用类型是堆存储，引用类型在栈中存放对象的地址，指向堆中的真实数据，如下图所示。栈是自动分配的内存空间，堆是动态分配的内存，大小不定也不会自动释放。
```
<img src="./assets/JS堆栈.png" style="width:250px; margin:0 auto">

* Null和Underfined的差异？
```
1、两者都代表无，在if判断语句中，值都为false；
2、Null转为数字类型值为0，而Underfined转为数字类型为NaN；
3、Null可以作为函数的参数，表示该函数的参数不是对象，同时Null也是对象原型链的终点；
4、Underfined表示变量别声明了但是没有赋值。
```

* var、let和const关键字的区别？
```
在ES6之前变量作用域只有全局作用域和局部（函数）作用域，没有块作用域，ES6新增let和const关键字来解决这一问题。
1、var只有全局作用域和局部作用域的概念，let和const只有块作用域的概念，由{}包括起来；
2、var存在变量提升，而let、const不存在变量提升，未声明时是无法访问该变量的；
3、const一旦声明必须赋值，声明后不能修改，如果声明的是对象，可以修改其属性；
4、同一作用域下let和const不能声明同名变量，而var可以。
```

* 为什么var可以重复声明？
```
编译器在遇到var关键字，会判断变量是否已经声明，如果已经声明则会忽略var直接对变量进行赋值。
```

* 深拷贝和浅拷贝的区别？
```
1、浅拷贝是复制了对象的引用地址，而非堆中的值，即两个对象指向同一个存储空间，修改其中一个对象的值另一个值也会改变，例如object.assign()；
2、深拷贝将对象及值复制过来，两个对象修改其中的值另一个值都不会改变，例如JSON.parse()和JSON.stringify()。
```
```
//自定义函数实现浅拷贝
function shallowCopy(src){
    var dest = {};
    for(var prop in src){
        if(src.hasOwnProperty(prop)){
            dest[prop] = src[prop];
        }
    }
    return dest;
}

//自定义函数实现深拷贝(递归)
function deepCopy(src){
    if(typeof src !== 'object') return;
    var dest = src instanceof Array ? [] : {};
    for(var prop in src){
        if(src.hasOwnProperty(prop)){
            dest[prop] = typeof src[prop] === 'object' ? deepCopy(src[prop]) : src[prop];
        }
    }
    return dest;
}
```

* typeof和instanceof有什么区别？

* 什么是闭包？
```
闭包就是能取其它函数内部变量的函数，作用：1、可以读取函数内部的变量；2、让这些变量的值始终保持在内存中。
由于闭包会使函数变量保存在内存中，所以在浏览器中可能会导致内存泄漏，解决方法是在退出函数时将不使用的局部变量删除。
```

* 谈谈This对象的理解？

* 什么是原型、原型链？

* JS继承的几种实现方式？

* JS创建对象的几种方式？

* new操作符具体干了什么？

* JS异步加载的几种方式？

* 什么是Promise？
```
Promise对象用于异步操作，表示一个尚未完成且预计在未来完成的异步操作。
```

* call、reply有什么区别？

* 事件监听、事件冒泡？

* 如何解决跨域问题？

* 谈谈你对ES6的了解？

* DOM操作？

* 如何编写高性能的JS？

* 哪些操作会造成内存泄露？

## VUE
* vue是如何实现双向绑定的？
```
1、vue2使用Object.defineProperty进行双向绑定，vue3使用proxy取代之。
```

* vue的组件通信？

* vue的diff算法？

* vue路由的实现原理？

## HTTP
* 平时遇到跨域问题都用什么解决方案？

## CSS 
*