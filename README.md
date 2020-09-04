# 前端面经
[JS](#JS)
* [JS数据类型有哪些？](#JS数据类型有哪些？)
* [Null和Undefined的差异？](#Null和Undefined的差异？)
* [var、let和const关键字的区别？](#var、let和const关键字的区别？)
* [为什么var可以重复声明？](#为什么var可以重复声明？)
* [JS中什么是变量提升？什么是暂时性死区？](#JS中什么是变量提升？什么是暂时性死区？)
* [深拷贝和浅拷贝的区别？](#深拷贝和浅拷贝的区别？)
* [什么是闭包？](#什么是闭包？)
* [typeof和instanceof有什么区别？](#typeof和instanceof有什么区别？)
* [什么是原型、原型链？](#什么是原型、原型链？)
* [如何正确判断this关键字的指向？](#如何正确判断this关键字的指向？)
* [JS继承的几种实现方式？](#JS继承的几种实现方式？)
* [JS创建对象的几种方式？](#JS创建对象的几种方式？)
* [new操作符具体干了什么？](#new操作符具体干了什么？)
* [call、apply和bind方法有什么区别？](#call、apply和bind方法有什么区别？)
* [JS异步加载的几种方式？](#JS异步加载的几种方式？)
* [什么是Promise？](#什么是Promise？)
* [事件监听、事件捕获、事件冒泡（事件委托机制）？](#事件监听、事件捕获、事件冒泡（事件委托机制）？)
* [Set、Map、WeakSet、WeakMap的区别？](#Set、Map、WeakSet、WeakMap的区别？)
* [谈谈你对ES6的了解（ES6的新特性）？](#谈谈你对ES6的了解（ES6的新特性）？)
* [防抖与节流？](#防抖与节流？)
* [函数柯里化？](#函数柯里化？)
* [什么是window对象，什么是document对象？](#什么是window对象，什么是document对象？)
* [sync/await的概念？](#sync/await的概念？)
* [如何编写高性能的JS？](#如何编写高性能的JS？)
* [哪些操作会造成内存泄露？](#哪些操作会造成内存泄露？)
* [谈谈你对模块化的理解？](#谈谈你对模块化的理解？)
* [webpack?](#webpack?)

[HTML](#HTML)

[VUE](#VUE)

[HTTP](#HTTP)

[CSS](#CSS)
* [页面导入样式时，使用link和@import的区别？](#页面导入样式时，使用link和@import的区别？)
* [伪类和伪元素的区别？](#伪类和伪元素的区别？)
* [CSS中position属性有哪些取值，它们的行为是什么？](#CSS中position属性有哪些取值，它们的行为是什么？)
* [圣杯布局的原理和实现方法？](#圣杯布局的原理和实现方法？)

## JS
### JS数据类型有哪些？
* 基本数据类型：String、Number、Boolean、Null、Undefined、Symbol（ES6新增，表示独一无二的值）；
* 引用类型：Object。
基本数据类型在内存中是栈存储，引用类型是堆存储，引用类型在栈中存放对象的地址，指向堆中的真实数据，如下图所示。栈是自动分配的内存空间，堆是动态分配的内存，大小不定也不会自动释放。

<img src="./assets/JS堆栈.png" style="width:250px; margin:0 auto">

### Null和Undefined的差异？
* 两者都代表无，在if判断语句中，值都为false；
* Null转为数字类型值为0，而Undefined转为数字类型为NaN；
* Null可以作为函数的参数，表示该函数的参数不是对象，同时Null也是对象原型链的终点；
* Undefined表示变量别声明了但是没有赋值。

### var、let和const关键字的区别？
在ES6之前变量作用域只有全局作用域和局部（函数）作用域，没有块作用域，ES6新增let和const关键字来解决这一问题。
* var只有全局作用域和局部作用域的概念，let和const只有块作用域的概念，由{}包括起来；
* var存在变量提升，而let、const不存在变量提升，未声明时是无法访问该变量的；
* const一旦声明必须赋值，声明后不能修改，如果声明的是对象，可以修改其属性；
* 同一作用域下let和const不能声明同名变量，而var可以。

### 为什么var可以重复声明？
* 编译器在遇到var关键字，会判断变量是否已经声明，如果已经声明则会忽略var直接对变量进行赋值。

### JS中什么是变量提升？什么是暂时性死区？
* 变量提升就是在声明之前就可以使用，值为undefined；而使用let/const声明变量前，该变量都是不可用的，语法上称为“暂时性死区”；
* 暂时性死区的本质就是变量已经存在但是不可获取，只有等到变量被声明时才能获取和使用该变量。
```
// 变量提升
typeof x;   //undefined，不会报错
var x;

// 暂时性死区
typeof y;   //ReferenceError(暂时性死区)
lex y;
```

### 深拷贝和浅拷贝的区别？
* 浅拷贝是复制了对象的引用地址，而非堆中的值，即两个对象指向同一个存储空间，修改其中一个对象的值另一个值也会改变，例如object.assign()；
* 深拷贝将对象及值复制过来，两个对象修改其中的值另一个值都不会改变，例如JSON.parse()和JSON.stringify()。
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

### 什么是闭包？
闭包就是能取其它函数内部变量的函数，作用：
* 可以读取函数内部的变量；
* 让这些变量的值始终保持在内存中。

由于闭包会使函数变量保存在内存中，所以在浏览器中可能会导致内存泄漏，解决方法是在退出函数时将不使用的局部变量删除。

### typeof和instanceof有什么区别？
JS中使用typeof和instanceof来判断一个变量是什么类型。
* typeof对于基本数据类型除了null（typeof null输出为对象）都可以显示正确类型，对于引用类型除了函数输出'function'，其它输出全是'object'，因此无法准确知道对象的类型；
* instanceof用来判断某个构造函数的prototype属性是否存在于检测对象的原型链上，即一个变量是否属于某个对象的实例，因此，instanceof只能正确判断引用类型。
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

### 什么是原型、原型链？
* 每个对象都有一个原型对象，通过__proto__指针指向其原型对象，并从中继承方法和属性，同时原型对象也可能拥有原型，这样一层一层最终指向null（原型链的终点，Object.prototype.__proto__指向null）。这种关系链被称为原型链，通过原型链一个对象可以继承其它对象的方法和属性，是实现继承的主要方式。
* 构造函数Parent、原型Parent.prototype和实例p之间的关系如下图所示（p.__proto__ === Parent.prototype）。
（注：prototype是构造函数的属性，__proto__是每个实例都有的属性，实例的__proto__与其构造函数的prototype指向同一个对象，即该实例的原型）
<img src="./assets/原型链.png" style="width:250px; margin:0 auto">

### 如何正确判断this关键字的指向？
this是一个指针，指向调用函数的对象，this有四种绑定规则：默认绑定、隐式绑定、显示绑定、new绑定。4种规则的优先级为：new绑定 > 显示绑定 > 隐式绑定 > 默认绑定。
* 默认绑定
* 隐式绑定
* 显示绑定
* new绑定

### JS继承的几种实现方式？
* 原型链继承，将父类的实例作为子类的原型；
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
```
* 借助构造函数实现继承；
```
// 2、构造函数继承
function Cat(name){
    Animal.call(this);
    this.name = name || 'Cat';
}
var cat = new Cat();
```
* 组合继承；
```
// 3、组合继承
function Cat(name){
    Animal.call(this);
    this.name = name || 'Cat';
}
Cat.prototype = new Animal();
var cat = new Cat();
```
* 寄生组合继承；
```
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
```
* class继承，开发中推荐使用的方式。
```
// 5、class继承
```
### JS创建对象的几种方式？
* 通过Object构造函数创建；
```
var Person = new Object();
```
* 使用对象字面量的方式创建（对象字面量是对象定义的一种简写形式）；
```
var Person = {
    name: 'Tom';
    age: 18;
}
```
* 使用工厂模式创建；
```
function createPerson(name, age, sex){
    var obj = new Object();
    obj.name = name;
    obj.age = age;
    obj.sex = sex;
    return obj;
}
var person = createPerson('Tom', 18, 'man');
```
* 使用构造函数创建；
```
function Person(name, age, sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
var person = new Person('Tom', 18, 'man');
```
* 使用原型对象创建
```
function Person(){}
Person.prototype.name = 'Tom';
Person.prototype.age = 18;
Person.prototype.sex = 'man';
var person = new Person();
```
* 组合使用构造函数和原型创建；
```
function Person(name, age, sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Person.prototype = {
    constructor: Person;
}
var person = new Person('Tom', 18, 'man');
```

### new操作符具体干了什么？
new操作可以分为以下4个步骤：
* 创建一个空对象； 
```
// 以var p = new Person()为例
const o = new Object();
```
* 将空对象的__proto__指向构造函数的prototype； 
```
o.__proto__ = Person.prototype;
```
* 将构造函数的this指向空对象，执行构造函数；   
```
var res = Person.call(o);
```
* 判断构造函数的返回值类型，返回新对象；   
```
return typeof res === 'object' ? res : o;
```

### call、apply和bind方法有什么区别？
它们的作用都是用来改变函数中this的指向。
* call和reply的区别在于两者的传参方式不同，除第一个参数都指向this，call的其它参数都会作为函数形参传入，而apply需要将其它参数包裹在数组中传入。
* bind的传参方式和call相同，但是call和apply方法调用后会立即执行，而bind方法调用后会返回一个新的函数，需要手动执行。

### JS异步加载的几种方式？
JS加载方式分为：
* 同步加载/阻塞加载，只有当前加载完成，才能进行下一步操作，默认同步加载是安全的，但可能会造成页面阻塞；
* 异步加载/非阻塞加载，浏览器在执行js的同时，还会继续对后续页面进行处理。

异步加载的方式主要有：
* Script DOM Element；
* onload时的异步加载

### 什么是Promise？   
* Promise对象用于异步操作，表示一个尚未完成且预计在未来完成的异步操作。

### 事件监听、事件捕获、事件冒泡（事件委托机制）？

### Set、Map、WeakSet、WeakMap的区别？
Set、Map、WeakSet、WeakMap是ES6新增的数据结构。
* Set：成员唯一、无序且不重复，可以遍历。
* WeakSet：成员唯一、无序且不重复，但是成员都是弱引用对象，不能遍历；
* Map：键值对，可以遍历；
* WeakMap：键值对，但是键名为弱引用对象，不能遍历。

### 谈谈你对ES6的了解（ES6的新特性）？
* 新增一种一本数据类型（Symbol）；
* 新增块作用域（let、const）；
* 新增定义类的语法糖（class）；
* 新增箭头函数；
* 新增数据结构（Set、Map、WeakSet、WeakMap）；
* 新增模块化（import/export）；
* 新增Proxy构造函数，用来生成proxy示例。

### 防抖与节流？
* 应用场景：对于短时间内连续触发的事件，例如scroll、mousemove等，不希望事件连续触发的过程中频繁地执行函数。
* 防抖：触发事件后在某个时间期限后，执行函数，如果在时间期限内又触发了事件，则会重新计时。
```
/**
*   fn 需要防抖的函数
*   delay 防抖期限值
*/
function debounce(fn, delay){
    let timeout = null;
    return function(){
        if(timeout){
            clearTimeout(timeout);
        }
        timeout = setTimeout(fn, delay);
    }
}
```

如果在时间期限内，不断触发事件，采用防抖的方法将会永远无法执行函数，因此需要新的方案。
* 节流：函数在执行一次后，该函数在指定的时间期限内将失效，直到过了这段时间才重新生效。
```
/**
*   fn 需要防抖的函数
*   delay 防抖期限值
*/
function throttle(fn, delay){
    let valid = true;
    return function(){
        if(!valid){
            return false;   //失效
        }
        valid = false;
        //也可以使用时间戳实现
        setTimeout(() => {
            fn();
            valid = true;
        }, delay);
    }
}
```

### 函数柯里化？
函数柯里化就是只传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数。示例：
```
// 普通的add函数
function add(x, y){
    return x + y;
}

// 柯里化后的add函数
function curryingAdd(x){
    return function(y){
        return x + y;
    }
}
```
函数柯里化的作用：
* 参数复用，减少代码冗余，增加可读性；
* 延迟运行，JS种bind的实现机制就是柯里化。
柯里化的实现方式：
```
function curry(fn, curArgs){
    return function(){
        let args = [].slice.call(arguments);
        if(curArgs !== undefined){
            args = args.concat(curArgs);
        }
        //递归调用
        if(args.length < fn.length){
            return curry(fn, args);
        }
        //递归出口
        return fn.apply(null, args);
    }
}

//测试
function sum(a, b, c){
    return a + b + c;
}
const fn = curry(sum);
fn(1, 2, 3);    //return 6
fn(1, 2)(3);    //return 6
fn(1)(2)(3);    //return 6
```

### 什么是window对象，什么是document对象？

### async/await的概念？

### 如何编写高性能的JS？
* 遵循严格模式："use strict"；

### 哪些操作会造成内存泄露？
内存泄漏是指不再需要的对象仍然存在于内存中，根据JS的垃圾回收机制，垃圾回收器会定时扫描对象，如果一个对象的引用计数为0，该对象的内存就会被回收。因此，如果一个不再需要的对象仍然被其它对象引用，就会造成内存泄漏。造成内存泄露的常见操作有：
* 全局变量；
* 闭包；
* 没有清理的DOM元素引用；
* 被遗忘的计时器或者回调函数；
* 循环引用。

### 谈谈你对模块化的理解？

### webpack?

## HTML
### 什么是DOM？

### script标签的defer和async是什么？

## VUE
### vue生命周期？

### vue是如何实现双向绑定的？
* vue2使用Object.defineProperty进行双向绑定，vue3使用proxy取代之。

### vue的组件通信？

### vue的diff算法？

### vue路由的实现原理？

## HTTP
### 平时遇到跨域问题都用什么解决方案？
跨域是指浏览器不能执行其它网站的脚本，是由浏览器的同源策略造成的。同源策略是浏览器最基本也是最核心的安全策略，所谓同源是指：协议、域名、端口号都相同，只要有一个不同，就是非同源。

跨域的常见解决方案有以下几种：
* 通过jsonp跨域；
* document.domain；
* nginx代理跨域；
* ...

### 从输入URL到展示的过程？
* DNS解析；
* TCP三次握手；
* 客户端发送请求；
* 

### TCP三次握手？

### HTTP和HTTPS协议的区别？

### 常见状态码？
1.消息；2.成功；3.重定向；4.请求错误；5.服务器错误。

### get和post的区别？

### Websocket？

## CSS 
### 页面导入样式时，使用link和@import的区别？
* link是XHTML标签，除了加载CSS之外，还能定义rel连接属性等作用，而@import由CSS提供，只能加载CSS；
* link引用CSS时，在页面载入时同时加载，而@import需要页面完全载入以后加载；
* link是XHTML标签，无兼容问题，而@import是CSS2.1提出的，低版本的浏览器不支持；
* link支持JS控制DOM去改变样式，而@import不支持。

### 伪类和伪元素的区别？
CSS规定伪类使用一个冒号(:)来表示，伪元素使用两个冒号(::)来表示。
* 常见的伪类有:hover, :active, :focus, :visited, :first-child, :last-child等；
* 常见的伪元素有::before, ::after等。

### CSS中position属性有哪些取值，它们的行为是什么？
position属性的常用取值有：static、fixed、absolute、relative。
* static，是position属性的默认值，指无特殊定位；
* fixed，相对浏览器窗口进行定位；
* absolute
* relative

### 圣杯布局的原理和实现方法？
圣杯布局解决的问题：中间宽度自适应、两边定宽的三栏布局，且中间栏要放在文档流前面优先渲染。

原理：使用浮动、相对定位和负边距。
```
// HTML代码
<div class="content">
    <div class="center col"></div>
    <div class="left col"></div>
    <div class="right col"></div>
</div>

// CSS代码
.content {
    padding: 0 100px;
}
.col {
    float: left;
    height: 200px;
    position: relative;
}
.left, .right {
    width: 100px;
}
.left {
    background: blue;
    margin-left: -100%;
    right: 100px;
}
.right {
    background: green;
    margin-left: -100px;
    left: 100px;
}
.center {
    width: 100%;
    background: pink;
}
```