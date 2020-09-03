# 前端面经
## JS
* JS数据类型有哪些？
```
1、基本数据类型：String、Number、Boolean、Null、Undefined、Symbol（ES6新增，表示独一无二的值）；
2、引用类型：Object。
基本数据类型在内存中是栈存储，引用类型是堆存储，引用类型在栈中存放对象的地址，指向堆中的真实数据，如下图所示。栈是自动分配的内存空间，堆是动态分配的内存，大小不定也不会自动释放。
```
<img src="./assets/JS堆栈.png" style="width:250px; margin:0 auto">

* Null和Undefined的差异？
```
1、两者都代表无，在if判断语句中，值都为false；
2、Null转为数字类型值为0，而Undefined转为数字类型为NaN；
3、Null可以作为函数的参数，表示该函数的参数不是对象，同时Null也是对象原型链的终点；
4、Undefined表示变量别声明了但是没有赋值。
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

* JS中什么是变量提升？什么是暂时性死区？
```
变量提升就是在声明之前就可以使用，值为undefined；而使用let/const声明变量前，该变量都是不可用的，语法上称为“暂时性死区”，暂时性死区的本质就是变量已经存在但是不可获取，只有等到变量被声明时才能获取和使用该变量。
```
```
// 变量提升
typeof x;   //undefined，不会报错
var x;

// 暂时性死区
typeof y;   //ReferenceError(暂时性死区)
lex y;
```

* 深拷贝和浅拷贝的区别？
```
1、浅拷贝是复制了对象的引用地址，而非堆中的值，即两个对象指向同一个存储空间，修改其中一个对象的值另一个值也会改变，例如object.assign()；
2、深拷贝将对象及值复制过来，两个对象修改其中的值另一个值都不会改变，例如JSON.parse()和JSON.stringify()。
```
```
// 自定义函数实现浅拷贝
function shallowCopy(src){
    var dest = {};
    for(var prop in src){
        if(src.hasOwnProperty(prop)){
            dest[prop] = src[prop];
        }
    }
    return dest;
}

// 自定义函数实现深拷贝(递归)
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
```
JS中使用typeof和instanceof来判断一个变量是什么类型。
1、typeof对于基本数据类型除了null（typeof null输出为对象）都可以显示正确类型，对于引用类型除了函数输出'function'，其它输出全是'object'，因此无法准确知道对象的类型；
2、instanceof用来判断某个构造函数的prototype属性是否存在于检测对象的原型链上，即一个变量是否属于某个对象的实例，因此，instanceof只能正确判断引用类型。
```
```
// instanceof实现代码(A instanceof B)
function instace_of(A, B){
    let prototype = B.prototype;
    while(true){
        if(A === null){    //找到A的原型链终点
            return false;
        }else if(A.__proto__ === prototype){
            return true;
        }else{
            A = A.__proto__;    //继续沿原型链向上查找
        }
    }
}
```

* 什么是原型、原型链？
```
每个对象都有一个原型对象，通过__proto__指针指向其原型对象，并从中继承方法和属性，同时原型对象也可能拥有原型，这样一层一层最终指向null（原型链的终点，Object.prototype.__proto__指向null）。这种关系链被称为原型链，通过原型链一个对象可以继承其它对象的方法和属性，是实现继承的主要方式。
构造函数Parent、原型Parent.prototype和实例p之间的关系如下图所示（p.__proto__ === Parent.prototype）。
（注：prototype是构造函数的属性，__proto__是每个实例都有的属性，实例的__proto__与其构造函数的prototype指向同一个对象，即该实例的原型）
```
<img src="./assets/原型链.png" style="width:250px; margin:0 auto">

* 什么是闭包？
```
闭包就是能取其它函数内部变量的函数，作用：1、可以读取函数内部的变量；2、让这些变量的值始终保持在内存中。
由于闭包会使函数变量保存在内存中，所以在浏览器中可能会导致内存泄漏，解决方法是在退出函数时将不使用的局部变量删除。
```

* 如何正确判断this关键字的指向？
```
this是一个指针，指向调用函数的对象，this有四种绑定规则：默认绑定、隐式绑定、显示绑定、new绑定。4种规则的优先级为：new绑定 > 显示绑定 > 隐式绑定 > 默认绑定。
1、默认绑定
2、隐式绑定
3、显示绑定
4、new绑定
```

* JS继承的几种实现方式？
```
1、原型链继承，将父类的实例作为子类的原型；
2、借助构造函数实现继承；
3、组合继承；
4、寄生组合继承；
5、class继承，开发中推荐使用的方式。
```
```
// 定义父类
function Animal(name){  
    this.name = name || 'Animal';    // 属性
    this.sleep = function(){}    // 实例方法
}
Animal.prototype.eat = function(food){}  // 原型方法

// 1、原型链继承
function Cat(){}    // 定义子类
Cat.prototype = new Animal();  // 将父类的实例作为子类的原型
Cat.prototype.name = 'Cat';

// 2、构造函数继承
function Cat(name){
    Animal.call(this);
    this.name = name || 'Cat';
}
var cat = new Cat();

// 3、组合继承
function Cat(name){
    Animal.call(this);
    this.name = name || 'Cat';
}
Cat.prototype = new Animal();
var cat = new Cat();

// 4、寄生组合继承
function Cat(name){
    Animal.call(this);
    this.name = name || 'Cat';
}
(function(){
    var Super = function(){};   //创建一个没有实例方法的类
    Super.prototype = Animal.prototype;
    Cat.prototype = new Super();    //将实例作为子类的原型
})();
var cat = new Cat();

// 5、class继承
```

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

* 谈谈你对ES6的了解（ES6的新特性）？
```
1、新增一种一本数据类型（Symbol）；
2、新增块作用域（let、const）；
```

* DOM操作？

* 如何编写高性能的JS？

* 哪些操作会造成内存泄露？

* webpack?

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