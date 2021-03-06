# 前端面经

[JS](#JS)

- [JS 数据类型有哪些？](#JS数据类型有哪些)
- [Null 和 Undefined 的差异？](#Null和Undefined的差异)
- [var、let 和 const 关键字的区别？](#varlet和const关键字的区别)
- [为什么 var 可以重复声明？](#为什么var可以重复声明)
- [JS 中什么是变量提升？什么是暂时性死区？](#JS中什么是变量提升？什么是暂时性死区)
- [深拷贝和浅拷贝的区别？](#深拷贝和浅拷贝的区别)
- [什么是闭包？](#什么是闭包)
- [typeof 和 instanceof 有什么区别？](#typeof和instanceof有什么区别)
- [什么是原型、原型链？](#什么是原型原型链)
- [如何正确判断 this 关键字的指向？](#如何正确判断this关键字的指向)
- [JS 继承的几种实现方式？](#JS继承的几种实现方式)
- [JS 创建对象的几种方式？](#JS创建对象的几种方式)
- [new 操作符具体干了什么？](#new操作符具体干了什么)
- [call、apply 和 bind 方法有什么区别？](#callapply和bind方法有什么区别)
- [JS 异步加载的几种方式？](#JS异步加载的几种方式)
- [什么是 Promise？](#什么是Promise)
- [async/await 的概念？](#asyncawait的概念)
- [JS 的事件捕获与事件冒泡？](#JS的事件捕获与事件冒泡)
- [JS 事件委托机制？](#JS事件委托机制)
- [JS 事件绑定的几种方式？](#JS事件绑定的几种方式)
- [Set、Map、WeakSet、WeakMap 的区别？](#SetMapWeakSetWeakMap的区别)
- [谈谈你对 ES6 的了解（ES6 的新特性）？](#谈谈你对ES6的了解ES6的新特性)
- [防抖与节流？](#防抖与节流)
- [函数柯里化？](#函数柯里化)
- [什么是 window 对象，什么是 document 对象？](#什么是window对象什么是document对象)
- [如何编写高性能的 JS？](#如何编写高性能的JS)
- [哪些操作会造成内存泄露？](#哪些操作会造成内存泄露)
- [谈谈你对模块化的理解？](#谈谈你对模块化的理解)
- [webpack?](#webpack)
- [JS 的事件循环机制以及微任务、宏任务？](#JS的事件循环机制以及微任务宏任务)
- [正则表达式总结](#正则表达式总结)

[HTML](#HTML)

- [HTML 行内元素和块级元素的区别？](#HTML行内元素和块级元素的区别)
- [什么是 DOM？](#什么是DOM)
- [什么是虚拟 DOM？](#什么是虚拟DOM)
- [浏览器是如何渲染页面的？](#浏览器是如何渲染页面的)
- [script 标签的 defer 和 async 属性有什么作用？](#script标签的defer和async属性有什么作用)
- [DOMContentLoaded 和 onload 的区别？](#DOMContentLoaded和onload的区别)

[HTTP](#HTTP)

- [平时遇到跨域问题都用什么解决方案？](#平时遇到跨域问题都用什么解决方案)
- [从输入 URL 到展示的过程？](#从输入URL到展示的过程)
- [TCP 三次握手与四次挥手](#TCP三次握手与四次挥手)
- [HTTP 和 HTTPS 协议的区别？](#HTTP和HTTPS协议的区别)
- [常见状态码？](#常见状态码)
- [get 和 post 的区别？](#get和post的区别)
- [Websocket 的使用场景？](#Websocket的使用场景)

[操作系统](#操作系统)

- [进程和线程的区别？](#进程和线程的区别)

[VUE](#VUE)

- [Vue 的生命周期？](#Vue的生命周期)
- [Vue 是如何实现双向绑定的？](#Vue是如何实现双向绑定的)
- [Vue 的组件通信？](#Vue的组件通信)
- [Vue 的 diff 算法？](#Vue的diff算法)
- [Vue 路由的实现原理？](#Vue路由的实现原理)

[CSS](#CSS)

- [页面导入样式时，使用 link 和@import 的区别？](#页面导入样式时使用link和import的区别)
- [伪类和伪元素的区别？](#伪类和伪元素的区别)
- [CSS 中 position 属性有哪些取值，它们的行为是什么？](#CSS中position属性有哪些取值它们的行为是什么)
- [CSS 中 display 属性有哪些取值，它们的行为是什么？](#CSS中display属性有哪些取值它们的行为是什么)
- [两栏布局的原理和实现方法？](#两栏布局的原理和实现方法)
- [圣杯布局的原理和实现方法？](#圣杯布局的原理和实现方法)
- [垂直居中如何实现？](#垂直居中如何实现)
- [CSS 样式优先级？](#CSS样式优先级)
- [CSS 盒子模型？](#CSS盒子模型)

[算法](#算法)

- [快速排序](#快速排序)
- [数组扁平化](#数组扁平化)
- [相交链表](#相交链表)
- [LeetCode](#LeetCode)

[工作总结](#工作总结)

- [内存泄漏](#内存泄漏)
- [排序算法优化](#排序算法优化)

## JS

### JS 数据类型有哪些？

- 基本数据类型：String、Number、Boolean、Null、Undefined、Symbol（ES6 新增，表示独一无二的值）；
- 引用类型：Object。
  基本数据类型在内存中是栈存储，引用类型是堆存储，引用类型在栈中存放对象的地址，指向堆中的真实数据，如下图所示。栈是自动分配的内存空间，堆是动态分配的内存，大小不定也不会自动释放。

<img src="./assets/JS堆栈.png" style="width:250px; margin:0 auto">

### Null 和 Undefined 的差异？

- 两者都代表无，在 if 判断语句中，值都为 false；
- Null 转为数字类型值为 0，而 Undefined 转为数字类型为 NaN；
- Null 可以作为函数的参数，表示该函数的参数不是对象，同时 Null 也是对象原型链的终点；
- Undefined 表示变量别声明了但是没有赋值。

### var、let 和 const 关键字的区别？

在 ES6 之前变量作用域只有全局作用域和局部（函数）作用域，没有块作用域，ES6 新增 let 和 const 关键字来解决这一问题。

- var 只有全局作用域和局部作用域的概念，let 和 const 只有块作用域的概念，由{}包括起来；
- var 存在变量提升，而 let、const 不存在变量提升，未声明时是无法访问该变量的；
- const 一旦声明必须赋值，声明后不能修改，如果声明的是对象，可以修改其属性；
- 同一作用域下 let 和 const 不能声明同名变量，而 var 可以。

```javascript
// var和let作用域的常见面试题
//知识点：JS的事件循环机制，setTimeout的机制
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 0);
}
//输出 10   共10个

for (let i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 0);
}
//输出 0 1 2 3 4 5 6 7 8 9
```

### 为什么 var 可以重复声明？

- 编译器在遇到 var 关键字，会判断变量是否已经声明，如果已经声明则会忽略 var 直接对变量进行赋值。

### JS 中什么是变量提升？什么是暂时性死区？

- 变量提升就是在声明之前就可以使用，值为 undefined；而使用 let/const 声明变量前，该变量都是不可用的，语法上称为“暂时性死区”；
- 暂时性死区的本质就是变量已经存在但是不可获取，只有等到变量被声明时才能获取和使用该变量。

```javascript
// 变量提升
typeof x;   //undefined，不会报错
var x;

// 暂时性死区
typeof y;   //ReferenceError(暂时性死区)
lex y;
```

### 深拷贝和浅拷贝的区别？

- 浅拷贝是复制了对象的引用地址，而非堆中的值，即两个对象指向同一个存储空间，修改其中一个对象的值另一个值也会改变，例如 object.assign()；
- 深拷贝将对象及值复制过来，两个对象修改其中的值另一个值都不会改变，例如 JSON.parse()和 JSON.stringify()。

```javascript
// 自定义函数实现浅拷贝
function shallowCopy(src) {
  var dest = {};
  for (var prop in src) {
    if (src.hasOwnProperty(prop)) {
      dest[prop] = src[prop];
    }
  }
  return dest;
}

// 自定义函数实现深拷贝(递归)
function deepCopy(src) {
  if (typeof src !== "object") return;
  var dest = src instanceof Array ? [] : {};
  for (var prop in src) {
    if (src.hasOwnProperty(prop)) {
      dest[prop] =
        typeof src[prop] === "object" ? deepCopy(src[prop]) : src[prop];
    }
  }
  return dest;
}
```

### 什么是闭包？

闭包就是能取其它函数内部变量的函数，作用：

- 可以读取函数内部的变量；
- 让这些变量的值始终保持在内存中。

由于闭包会使函数变量保存在内存中，所以在浏览器中可能会导致内存泄漏，解决方法是在退出函数时将不使用的局部变量删除。

### typeof 和 instanceof 有什么区别？

JS 中使用 typeof 和 instanceof 来判断一个变量是什么类型。

- typeof 对于基本数据类型除了 null（typeof null 输出为对象）都可以显示正确类型，对于引用类型除了函数输出'function'，其它输出全是'object'，因此无法准确知道对象的类型；
- instanceof 用来判断某个构造函数的 prototype 属性是否存在于检测对象的原型链上，即一个变量是否属于某个对象的实例，因此，instanceof 只能正确判断引用类型。

```javascript
// instanceof实现代码(A instanceof B)
function instace_of(A, B) {
  let prototype = B.prototype;
  while (true) {
    if (A === null) {
      //找到A的原型链终点
      return false;
    } else if (A.__proto__ === prototype) {
      return true;
    } else {
      A = A.__proto__; //继续沿原型链向上查找
    }
  }
}
```

### JS 中判断数据类型的方式？

- typeof；
- instanceof；
- constructor，返回对象相应的构造函数（对于构造函数 Parent，Parent.prototype.constructor === Parent;&nbsp;&nbsp;//true）；
- Object.prototype.toString，toString 方法默认返回调用者的具体类型，更严格的讲就是 this 指向的对象类型。必须通过 Object.prototype.toString 来查找，而不能直接使用 toString 方法，是因为直接调用 toString 方法，实际上调用的重写后的方法，而不是 Object.prototype 中的 toString 方法。

### 什么是原型、原型链？

- 每个对象都有一个原型对象，通过 \_\_proto\_\_ 指针指向其原型对象，并从中继承方法和属性，同时原型对象也可能拥有原型，这样一层一层最终指向 null（原型链的终点，Object.prototype.\_\_proto\_\_指向 null）。这种关系链被称为原型链，通过原型链一个对象可以继承其它对象的方法和属性，是实现继承的主要方式。
- 构造函数 Parent、原型 Parent.prototype 和实例 p 之间的关系如下图所示（p.**proto** === Parent.prototype;&nbsp;&nbsp;//true）。
  （注：prototype 是构造函数的属性，\_\_proto\_\_ 是每个实例都有的属性，实例的 \_\_proto\_\_ 与其构造函数的 prototype 指向同一个对象，即该实例的原型）
  <img src="./assets/原型链.png" style="width:250px; margin:0 auto">

### 如何正确判断 this 关键字的指向？

this 是一个指针，指向调用函数的对象，this 有四种绑定规则：默认绑定、隐式绑定、显示绑定、new 绑定。4 种规则的优先级为：new 绑定 > 显示绑定 > 隐式绑定 > 默认绑定。

- 默认绑定
- 隐式绑定
- 显示绑定
- new 绑定

### JS 继承的几种实现方式？

- 原型链继承，将父类的实例作为子类的原型；

```javascript
// 定义父类
function Animal(name) {
  this.name = name || "Animal"; // 属性
  this.sleep = function() {}; // 实例方法
}
Animal.prototype.eat = function(food) {}; // 原型方法

// 1、原型链继承
function Cat() {} // 定义子类
Cat.prototype = new Animal(); // 将父类的实例作为子类的原型
Cat.prototype.name = "Cat";
```

- 借助构造函数实现继承；

```javascript
// 2、构造函数继承
function Cat(name) {
  Animal.call(this);
  this.name = name || "Cat";
}
var cat = new Cat();
```

- 组合继承；

```javascript
// 3、组合继承
function Cat(name) {
  Animal.call(this);
  this.name = name || "Cat";
}
Cat.prototype = new Animal();
var cat = new Cat();
```

- 寄生组合继承；

```javascript
// 4、寄生组合继承
function Cat(name) {
  Animal.call(this);
  this.name = name || "Cat";
}
(function() {
  var Super = function() {}; //创建一个没有实例方法的类
  Super.prototype = Animal.prototype;
  Cat.prototype = new Super(); //将实例作为子类的原型
})();
var cat = new Cat();
```

- class 继承，开发中推荐使用的方式。

```javascript
// 5、class继承
```

### JS 创建对象的几种方式？

- 通过 Object 构造函数创建；

```javascript
var Person = new Object();
```

- 使用对象字面量的方式创建（对象字面量是对象定义的一种简写形式）；

```javascript
var Person = {
    name: 'Tom';
    age: 18;
}
```

- 使用工厂模式创建；

```javascript
function createPerson(name, age, sex) {
  var obj = new Object();
  obj.name = name;
  obj.age = age;
  obj.sex = sex;
  return obj;
}
var person = createPerson("Tom", 18, "man");
```

- 使用构造函数创建；

```javascript
function Person(name, age, sex) {
  this.name = name;
  this.age = age;
  this.sex = sex;
}
var person = new Person("Tom", 18, "man");
```

- 使用原型对象创建

```javascript
function Person() {}
Person.prototype.name = "Tom";
Person.prototype.age = 18;
Person.prototype.sex = "man";
var person = new Person();
```

- 组合使用构造函数和原型创建；

```javascript
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

### new 操作符具体干了什么？

new 操作可以分为以下 4 个步骤：

- 创建一个空对象；

```javascript
// 以var p = new Person()为例
const o = new Object();
```

- 将空对象的**proto**指向构造函数的 prototype；

```javascript
o.__proto__ = Person.prototype;
```

- 将构造函数的 this 指向空对象，执行构造函数；

```javascript
var res = Person.call(o);
```

- 判断构造函数的返回值类型，返回新对象；

```javascript
return typeof res === "object" ? res : o;
```

### call、apply 和 bind 方法有什么区别？

它们的作用都是用来改变函数中 this 的指向。

- call 和 reply 的区别在于两者的传参方式不同，除第一个参数都指向 this，call 的其它参数都会作为函数形参传入，而 apply 需要将其它参数包裹在数组中传入。
- bind 的传参方式和 call 相同，但是 call 和 apply 方法调用后会立即执行，而 bind 方法调用后会返回一个新的函数，需要手动执行。

### JS 异步加载的几种方式？

JS 加载方式分为：

- 同步加载/阻塞加载，只有当前加载完成，才能进行下一步操作，默认同步加载是安全的，但可能会造成页面阻塞；
- 异步加载/非阻塞加载，浏览器在执行 js 的同时，还会继续对后续页面进行处理。

异步加载的方式主要有：

- Script DOM Element；
- onload 时的异步加载；
- script 标签的 defer 和 async 属性；

### 什么是 Promise？

- Promise 对象用于异步操作，表示一个尚未完成且预计在未来完成的异步操作。
- Promise 对象的状态不受外界影响，有三种状态：<br>
  （1）pending：初始状态；<br>
  （2）fulfilled：已成功；<br>
  （3）rejected：已失败。<br>
  只有异步操作的结果可以决定当前是哪一种状态，而且一旦状态改变就不会再变，即 Promise 对象状态只能由 pending 变成 fulfilled，或由 pending 变成 rejected；
- new Promise 在实例化过程中执行的代码是同步进行的，then 中的回调才是异步执行的（所有会进入异步的都是指事件回调中的那部分代码）。

```javascript
// 基础用法
const p1 = new Promise(function(resolve, reject){
    if(//异步操作成功){
        resolve(value);
    }else{
        reject(error);
    }
});

p1.then(
    //success
    function(value){},
    //failure
    function(error){}
);
```

Promise 对象的几个重要方法：

- Promise.all()，方法接收一个数组作为参数，p1、p2、p3 都是 Promise 实例，p 的状态要变成 fulfilled，只有 p1、p2、p3 的状态都变成 fulfilled，否则 p 的状态就变成 rejected（类似于电路中的串联）；

```javascript
// 示例
const p = Promise.all([p1, p2, p3]);
```

- Promise.race()，方法也接收一个数组作为参数，p1、p2、p3 中哪个状态先发生改变，无论成功或失败，p 的状态也会跟着它改变；

```javascript
// 示例
const p = Promise.all([p1, p2, p3]);
```

- Promise.resolve()，将现有对象转换成 Promise 对象，该实例状态为 fulfilled；
- Promise.reject()，返回一个 Promise 实例，该实例状态为 rejected。

### Promise 为什么可以链式调用？

### async/await 的概念？

- async/await 实际上就是 Generator 的语法糖，在函数前加上 async 关键字表示将函数声明为异步函数，await 表示等待一个异步方法执行完成；
- async 函数返回一个 Promise 对象，return 返回值就是 then 方法中回调函数的参数；
- async 函数被调用后会立即执行，一旦遇到 await 就会先返回，等到异步操作执行完成后，再接着执行函数体后面的语句；

### JS 的事件捕获与事件冒泡？

事件就是文档或浏览器窗口发生的一些特定交互瞬间，比如用户点击页面的某个内容，某个页面加载完成等。<br>
事件流描述的是从页面中接收事件的顺序，IE 提出的是冒泡流，Netscape 提出的是捕获流，两者截然相反。

- 事件捕获：事件开始由不太具体的节点接收，然后逐级向下传播到最具体的元素；
- 事件冒泡：事件开始由最具体的元素接收，然后逐级向上传播到较不具体的节点；
- DOM 事件流的三个阶段：事件捕获阶段、处于目标阶段、事件冒泡阶段。示意图如下图所示。<br>
  <img src="./assets/DOM事件流.png" style="width:200px; margin:0 auto">

### JS 事件委托机制？

应用场景：很多 DOM 节点都需要监听的情况，如果给每个 DOM 节点都绑定监听函数，对性能会有极大影响，可以利用事件委托来解决这一问题。<br>
事件委托：利用事件冒泡的机制，委托父节点代为执行事件。

```javascript
// 示例（为每个子节点li添加点击事件）
<ul id="ul">
  <li>1</li>
  <li>2</li>
  <li>3</li>
</ul>;

// 不利用事件委托机制实现
// 当li数量很多时，性能将会很差
window.onload = function() {
  var Li = document.getElementById("ul").getElementsByTagName("li");
  for (let i = 0; i < Li.length; i++) {
    Li[i].onclick = function() {
      // 触发操作
    };
  }
};

// 利用事件委托机制实现
// 只需要对父节点添加事件
window.onload = function() {
  var Ul = document.getElementById("ul");
  Ul.onclick = function(event) {
    var e = event || window.event;
    var target = e.target || e.srcElement;
    if (target.nodeName.toLowerCase() === "li") {
      // 触发操作
    }
  };
};
```

### JS 事件绑定的几种方式？

JS 中三种常用的绑定事件的方法：

- 在 DOM 元素中直接绑定，例如：

```javascript
<input onclick="" type="button" />
```

- 在 JavaScript 代码中绑定，例如：

```javascript
<input id="input" type="button" />
<script type="text/javascript">
    document.getElementById("input").onclick = function(){}
</script>
```

- 绑定事件监听函数，addEventListener()或 attachEvent()，语法：

```javascript
elementObject.addEventListener(eventName, handle, useCapture); //参数useCapture指是否使用事件捕获，默认为false
elementObject.attachEvent(eventName, handle);
```

### Set、Map、WeakSet、WeakMap 的区别？

Set、Map、WeakSet、WeakMap 是 ES6 新增的数据结构。

- Set：成员唯一、无序且不重复，可以遍历。
- WeakSet：成员唯一、无序且不重复，但是成员都是弱引用对象，不能遍历；
- Map：键值对，可以遍历；
- WeakMap：键值对，但是键名为弱引用对象，不能遍历。

### 谈谈你对 ES6 的了解（ES6 的新特性）？

- 新增一种一本数据类型（Symbol）；
- 新增块作用域（let、const）；
- 新增定义类的语法糖（class）；
- 新增箭头函数；
- 新增数据结构（Set、Map、WeakSet、WeakMap）；
- 新增模块化（import/export）；
- 新增 Proxy 构造函数，用来生成 proxy 示例；
- 新增 Promise 对象。

### 防抖与节流？

- 应用场景：对于短时间内连续触发的事件，例如 scroll、mousemove 等，不希望事件连续触发的过程中频繁地执行函数。
- 防抖：触发事件后在某个时间期限后，执行函数，如果在时间期限内又触发了事件，则会重新计时。

```javascript
/**
 *   fn 需要防抖的函数
 *   delay 防抖期限值
 */
function debounce(fn, delay) {
  let timeout = null;
  return function() {
    if (timeout) {
      clearTimeout(timeout);
    }
    timeout = setTimeout(fn, delay);
  };
}
```

如果在时间期限内，不断触发事件，采用防抖的方法将会永远无法执行函数，因此需要新的方案。

- 节流：函数在执行一次后，该函数在指定的时间期限内将失效，直到过了这段时间才重新生效。

```javascript
/**
 *   fn 需要防抖的函数
 *   delay 防抖期限值
 */
function throttle(fn, delay) {
  let valid = true;
  return function() {
    if (!valid) {
      return false; //失效
    }
    valid = false;
    //也可以使用时间戳实现
    setTimeout(() => {
      fn();
      valid = true;
    }, delay);
  };
}
```

### 函数柯里化？

函数柯里化就是只传递给函数一部分参数来调用它，让它返回一个函数去处理剩下的参数。示例：

```javascript
// 普通的add函数
function add(x, y) {
  return x + y;
}

// 柯里化后的add函数
function curryingAdd(x) {
  return function(y) {
    return x + y;
  };
}
```

函数柯里化的作用：

- 参数复用，减少代码冗余，增加可读性；
- 延迟运行，JS 种 bind 的实现机制就是柯里化。
  柯里化的实现方式：

```javascript
function curry(fn, curArgs) {
  return function() {
    let args = [].slice.call(arguments);
    if (curArgs !== undefined) {
      args = args.concat(curArgs);
    }
    //递归调用
    if (args.length < fn.length) {
      return curry(fn, args);
    }
    //递归出口
    return fn.apply(null, args);
  };
}

//测试
function sum(a, b, c) {
  return a + b + c;
}
const fn = curry(sum);
fn(1, 2, 3); //return 6
fn(1, 2)(3); //return 6
fn(1)(2)(3); //return 6
```

### 什么是 window 对象，什么是 document 对象？

### 如何编写高性能的 JS？

- 遵循严格模式："use strict"；

### 哪些操作会造成内存泄露？

内存泄漏是指不再需要的对象仍然存在于内存中，根据 JS 的垃圾回收机制，垃圾回收器会定时扫描对象，如果一个对象的引用计数为 0，该对象的内存就会被回收。因此，如果一个不再需要的对象仍然被其它对象引用，就会造成内存泄漏。造成内存泄露的常见操作有：

- 全局变量；
- 闭包；
- 没有清理的 DOM 元素引用；
- 被遗忘的计时器或者回调函数；
- 循环引用。

### 谈谈你对模块化的理解？

### webpack?

### JS 的事件循环机制以及微任务、宏任务？

JS 是单线程、非阻塞的语言，单线程指 JS 中只有一个主线程来处理所有的任务（保证程序执行的一致性），非阻塞指当需要执行一项异步任务时，主线程会挂起（pending）这个任务，在异步任务返回结果时再执行相应的回调。

- 所有任务可以分为同步任务和异步任务。同步任务即立即执行的任务，会进入主线程中执行；异步任务即异步执行的任务，通过任务队列的机制协调；
- JS 是单线程的，但浏览器是多线程的。

JS 通过事件循环（Event Loop）来实现异步，过程如下图所示：<br>
<img src="./assets/JS事件循环.png" style="width:200px; margin:0 auto">

微任务和宏任务都是异步任务，常用的微任务和宏任务有：

- 微任务：原生 Promise，process.nextTick，Object.observe（已废弃），MutationObserver（已废弃），MessageChannel（Vue 中 nextTick 实现原理）；
- 宏任务：script 整体，setTimeout，setInterval，setImmediate，I/O；

微任务和宏任务的执行过程如下图所示：<br>
<img src="./assets/微任务与宏任务.png" style="width:200px; margin:0 auto">

### 正则表达式总结

1. 正则声明方式

- 构造函数申明：通过 RegExp 构造函数声明一个正则表达式对象，第一个参数是正则内容，第二个参数是修饰符。修饰符有 6 个：<br>
  （1）i，表示忽略大小写匹配；<br>
  （2）g，表示全局匹配，即匹配到一个后继续匹配，直到结束；<br>
  （3）m，多行匹配，即遇到换行仍然继续匹配，直到结束；<br>
  （4）s，表示允许 . 匹配换行符；<br>
  （5）u，表示使用 Unicode 码的模式进行匹配；<br>
  （6）y，表示“粘性”搜索，匹配从目标字符串的当前位置开始。<br>
  6 个修饰符既可以单独使用，也可以按任意顺序一起使用。

```javascript
// 例如
var reg = new RegExp("w", "gi");
```

- 字面量方式：最常见的一种声明方式，两个斜线内为正则内容，后面可以跟修饰符。

```javascript
// 例如
var reg = /\w/gi;
```

2. 正则表达式相关符号

- 方括号 [ ] ：用于查找方括号内任意字符；

```javascript
// 例如
[0 - 9][a - z]; //匹配单个数字 //匹配单个小写字符
```

- 大括号 { } ：
- 括号 ( ) ：
- ^ ：匹配输入的开始，^ 在 [ ] 内开始位置时表示匹配不在 [ ] 内的任意字符；
- \$ ：匹配输入的结束；
- \* ：匹配前一个表达式 0 次或多次，等价于 {0, }；
- \+ ：匹配前一个表达式 1 次或多次，等价于 {1, }；
- \? ：匹配前一个表达式 0 次或 1 次，等价于 {0, 1}；
- . ：匹配任意单个字符，除了换行和结束符；
- \w ：匹配任意单个单词字符（数字、字母、下划线），等价于 [A-Za-z0-9_] ；
- \W ：匹配任意单个非单词字符，与 \w 作用相反，等价于 [^a-za-z0-9_] ；
- \d ：匹配单个数字，等价于 [0-9] ；
- \D ：匹配单个非数字，与 \d 作用相反，等价于 [^0-9] ；
- \s ：匹配单个空白字符（\n，\f，\r，\t，\v）；
- \S ：匹配单个非空白字符，与 \s 作用相反；
- \b ：匹配单词边界，连续的数字、字母或下划线组成的字符串是一个单词；
- \B ：匹配非单词边界；
- \0 ：匹配 NULL 字符；
- \n ：匹配换行符；
- \f ：匹配换页符；
- \r ：匹配回车符；
- \t ：匹配制表符，tab 对应的字符；
- \v ：匹配垂直制表符；

3. 正则表达式相关方法

- RegExp 对象相关方法：<br>
  （1）test：判断是否匹配，返回 true/false；<br>
  （2）exec：返回匹配的结果，返回数组/null；
- String 对象相关方法：<br>
  （1）match：返回匹配的结果，非全局匹配时与 exec 返回结果一致，全局匹配时一次性返回所有匹配结果，返回数组/null；<br>
  （2）replace：将字符串中根据正则表达式匹配到的子串替换成其它子串，返回替换后的字符串；<br>
  （3）search：查找第一次匹配子串的位置，返回索引，未找到就返回 -1 ；<br>
  （4）split：将字符串根据规则拆分为数组，返回数组。

4. 常见的正则表达式使用案例

- 手机号匹配：以 1 开头，第二位为 3、5、7、8，且长度为 11 的数字组合；

```javascript
var reg = /^1[3578]\d{9}$/;
```

- 邮箱匹配

## HTML

### HTML 行内元素和块级元素的区别？

- 行内元素（内联元素）：和其它行内元素在同一行，不可设置宽高，只能容纳文本或者其它行内元素；
- 块级元素：总是在新的一行开始排列，可以设置宽高，可以容纳其它块级元素和行内元素；
- 可以通过修改 display 属性对行内元素和块级元素进行切换；
- 常见行内元素：a、span、img、input、textarea、select、button 等；
- 常见块级元素：div、p、h1~h6、ul、li、header、footer、section 等。

### 什么是 DOM？

DOM，即文档对象模型。DOM 将 HTML 文档表达为树结构（DOM 树、CSSOM 树、渲染树），可以通过 DOM 访问和操作 HTML 文档的内容。

### 什么是虚拟 DOM？

虚拟 DOM（Virtual DOM），即虚拟节点。首先需要明白为什么要使用虚拟 DOM，为实现数据变化时页面也随之变化，有如下几种实现方式：

- 重新构建整个 DOM 树，重新渲染；（效率低下）
- 遍历整个 DOM 树，查找数据变化的节点，重新渲染该节点；（实现困难）
- 当数据变化时，建立新的虚拟 DOM 树，比较新的虚拟 DOM 树和旧的虚拟 DOM 树的差异，将差异运用到真正的 DOM 树上。（实现简单，效率较高）

Virtual DOM 算法的实现过程：

- 用 JS 对象模拟 DOM 树；
- 比较新旧虚拟 DOM 树的差异（Virtual DOM 的 diff 算法）；
- 将差异运用到真正的 DOM 树上。

[深度剖析：如何实现一个 Virtual DOM 算法 #13](https://github.com/livoras/blog/issues/13)

### 浏览器是如何渲染页面的？

浏览器从 HTTP 服务器获取响应报文（HTML 文档），到呈现页面给用户，分为如下几个步骤：

- 构建 DOM 树，DOM 树是以 HTMLDocument 为根节点，其余节点为子节点组成的一棵树，示意图如下图所示。<br>
  <img src="./assets/DOM树.png" style="width:200px; margin:0 auto"><br>
  HTML 解释器将 HTML 文档构建为 DOM 树的过程过下：<br>
  （1）字节流（Bytes）；<br>
  （2）被解码为字符流（Characters）；<br>
  （3）被词法解析器解释成词语（Tokens）；<br>
  （4）被语法分析器构建成各种节点；<br>
  （5）组建成一棵 DOM 树。<br>
  在 HTML 解释器构建 DOM 树过程，可能会有 JavaScript 代码需要下载和执行，而 JavaScript 代码的下载和执行会阻塞文档的解析。因此，为防止页面阻塞，可以合理使用 script 标签的 defer 和 async 属性，或者将 script 元素放在 body 元素的最后面，提高用户体验。

- 构建 CSSOM 树，构建 DOM 树过程中文档 head 遇到 link 标记引用外部 CSS 样式表，会进行 CSSOM 树的构建。CSSOM 树和 DOM 树构建过程相同，CSSOM 树生成节点时，每个节点首先会继承父节点的所有样式，然后根据优先级对样式进行覆盖。
- 构建渲染树，渲染树由 DOM 树和 CSSOM 树合并而成；
- 布局与绘制页面<br>
  布局：浏览器按照从上到下、从左到右的顺序读取渲染树的节点，放到文档流上，如果节点 A 是节点 B 的子节点，在放入文档流时就应该将节点 A 按顺序放入到节点 B 的内部，这样浏览器就计算出了每个节点该放在页面哪个位置。<br>
  绘制：布局完成后，浏览器就将所有节点绘制出来，完成页面的渲染。

### script 标签的 defer 和 async 属性有什么作用？

HTML 解释器在构建 DOM 树过程中，如果遇到 script 标签（没有 defer 或 async 属性），会立即加载并执行其中的 JavaScript 代码，造成文档解析的阻塞。script 标签的 defer 和 async 属性能使解释器异步加载 JavaScript 代码。

- defer：文档解析和 JavaScript 代码的加载（不执行）是异步执行的，JavaScript 代码的执行需要等到文档中所有元素解析完成之后，DOMContentLoaded 事件触发执行之前。如果存在多个 defer 属性的 JavaScript 代码，它们按照加载顺序执行；
- async：文档解析和 JavaScript 代码的加载是异步执行的，JavaScript 代码加载完成后会立即执行，此时文档解析会停止。

### DOMContentLoaded 和 onload 的区别？

DOMContentLoaded 在 HTML 文档加载和解析完成之后触发，无需等待样式表、图像和子框架的完成加载，而 onload 在 HTML 所有相关资源被加载完成后触发。

## HTTP

### 平时遇到跨域问题都用什么解决方案？

跨域是指浏览器不能执行其它网站的脚本，是由浏览器的同源策略造成的。同源策略是浏览器最基本也是最核心的安全策略，所谓同源是指：协议、域名、端口号都相同，只要有一个不同，就是非同源。

跨域的常见解决方案有以下几种：

- 通过 jsonp 跨域；
- document.domain；
- nginx 代理跨域；
- ...

### 从输入 URL 到展示的过程？

- DNS 解析，为方便用户访问互联网，Internet 将域名和 IP 地址进行映射，用户可以通过域名访问网站，而不用去记住它的 IP 地址。通过域名得到主机对应的 IP 地址的过程就是 DNS 解析；<br>
  DNS 查询的两种方式：递归查询和迭代查询；
- TCP 三次握手；
- 客户端（浏览器）发送 HTTP 请求；
- 服务器处理请求并返回 HTTP 报文；
- 浏览器根据响应报文对页面进行渲染；
- 断开 TCP 连接。

### TCP 三次握手与四次挥手？

三次握手即 TCP 连接的建立，具体过程如下：

- xxx

四次挥手即 TCP 连接的释放，具体过程如下：

- xxx

### HTTP 和 HTTPS 协议的区别？

### 常见状态码？

HTTP 状态码表示服务器对 HTTP 请求的响应状态，由 3 位数字和原因短语组成，数字中第一位指定响应类别，根据响应类别可分为以下 5 种：

- 1xx：消息，接受的请求正在处理；
- 2xx：成功，请求正常处理完毕；
- 3xx：重定向，需要进行附加操作以完成请求；
- 4xx：请求错误，客户端请求出错；
- 5xx：服务器错误，服务器处理请求出错。

各类别常见的状态码：

- 200 OK：（从客户端发送给服务器）请求被正常处理并返回；
- 204 No Content：请求被成功处理，但响应报文没有资源可以返回；
- 206 Partial Content：对部分数据区间的数据发送请求，成功执行并返回指定范围的数据；
- 301 Moved Permanently：永久性重定向，请求的资源被分配了新的 URL，之后应使用新的 URL；
- 302 Found：临时性重定向，请求的资源被分配了新的 URL，希望本次使用新的 URL；
- 303 See Other：请求的资源被分配了新的 URL，应使用 GET 方法获取请求资源；
- 304 Not Modified：客户端发送带条件的 GET 请求，而自上次访问以来或根据请求条件，响应内容没有发生改变，服务器返回该状态码；
- 400 Bad Request：请求报文中存在语法错误；
- 401 Unauthorized：未经许可，需要经过 HTTTP 认证；
- 403 Forbidden：服务器拒绝本次访问，访问权限出现问题；
- 404 Not Found：服务器上无法找到请求的资源；
- 500 Internal Server Error：服务器在执行请求时发生错误；
- 503 Service Unavailable：服务器因维护或超负载停机，无法处理请求。

### get 和 post 的区别？

### Websocket 的使用场景？

## 操作系统

### 进程和线程的区别？

## VUE

### Vue 的生命周期？

### Vue 是如何实现双向绑定的？

- vue2 使用 Object.defineProperty 进行双向绑定，vue3 使用 proxy 取代之。

### Vue 的组件通信？

### Vue 的 diff 算法？

### Vue 路由的实现原理？

前端路由的一个核心就是更新视图但不重新请求页面，实现方式主要有两种：

- 利用 URL 中的 hash（"#"）；
- 利用 History API 在 HTML5 中新增的方法。

## CSS

### 页面导入样式时，使用 link 和@import 的区别？

- link 是 XHTML 标签，除了加载 CSS 之外，还能定义 rel 连接属性等作用，而@import 由 CSS 提供，只能加载 CSS；
- link 引用 CSS 时，在页面载入时同时加载，而@import 需要页面完全载入以后加载；
- link 是 XHTML 标签，无兼容问题，而@import 是 CSS2.1 提出的，低版本的浏览器不支持；
- link 支持 JS 控制 DOM 去改变样式，而@import 不支持。

### 伪类和伪元素的区别？

CSS 规定伪类使用一个冒号(:)来表示，伪元素使用两个冒号(::)来表示。

- 常见的伪类有:hover, :active, :focus, :visited, :first-child, :last-child 等；
- 常见的伪元素有::before, ::after 等。

### CSS 中 position 属性有哪些取值，它们的行为是什么？

position 属性的常用取值有：static、fixed、absolute、relative。

- static，是 position 属性的默认值，指无特殊定位；
- fixed，相对浏览器窗口进行定位；
- absolute，绝对定位，相对于 static 定位之外的第一个父元素进行定位；
- relative，相对定位，相对于正常位置进行定位。

### CSS 中 display 属性有哪些取值，它们的行为是什么？

### 两栏布局的原理和实现方法？

两栏布局：左侧栏定宽，右侧栏自适应。实现方式：

- float + margin；

```javascript
// HTML代码
<div class="left"></div>
<div class="right"></div>
```

### 圣杯布局的原理和实现方法？

圣杯布局解决的问题：中间宽度自适应、两边定宽的三栏布局，且中间栏要放在文档流前面优先渲染。

原理：使用浮动、相对定位和负边距。

```javascript
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

### 垂直居中如何实现？

### CSS 样式优先级？

HTML 中的 style 样式>内联样式>外部样式>用户设置>浏览器默认样式

### CSS 盒子模型？

盒子模型就是把 HTML 元素看作一个矩形的盒子，每个矩形都由元素的内容（content）、内边距（padding）、边框（border）和外边距（margin）组成。矩形盒子描述了一个文档元素在页面布局中的位置和大小。下图就是盒子模型的示意图：<br>
<img src="./assets/CSS盒子模型.png" style="width:200px; margin:0 auto">

- 每个盒子都有内容、内边距、边框、外边距 4 个属性，每个属性都包括上、右、下、左 4 个部分；
- content，即设置盒子的宽度（width）和高度（height）；
- padding：上 右 下 左（取值个数不同，表示的意思也不同）；
- border：border-width || border-style || border-color（综合写法，3 个子属性的顺序不能写错）；
- margin：上 右 下 左（取值个数不同，表示的意思也不同），margin 属性存在外边距合并现象，即：<br>
  （1）上下相邻的块元素垂直外边距合并：上下相邻的两个块元素，如果上面的元素有下外边距 margin-bottom，同时下面的元素有上外边距 margin-top，那么它们之间的垂直间距不是 margin-bottom 与 margin-top 之和，而是两者中的较大者；<br>
  （2）嵌套块元素垂直外边距合并：两个父子关系的块元素，如果父元素上内边距和边框，父元素的上外边距会与子元素的上外边距发生合并，合并的外边距为两者中的较大者。
- 根据盒子模型布局的稳定性，应该优先使用 width 和 height，其次使用 padding，再考虑使用 margin。

其它与盒子模型相关的属性：

- border-radius（圆角边框）：上 右 下 左（取值个数不同，表示的意思也不同）；
- box-shadow（盒子阴影）：h-shadow v-shadow blur spread color inset（前两个取值必须，其余可以省略）。

### BFC？

## 算法

### 快速排序

### 数组扁平化

将一个多维数组变为一个一维数组，例如：[1, 2, [3, [4, 5]]] --> [1, 2, 3, 4, 5]。

```javascript
// 1.递归
function flatten(arr){
    var res = [];
    for(let i = 0; i < arr.length; i++){
        if(Array.isArray(arr[i])){
            res = res.concat(flatten(arr[i]));
        }else{
            res.push(arr[i]);
        }
    }
    return res;
}

// 2.toString & split
function flatten(arr){
    return arr.toString().split(',').map(function(item){
        return parseInt(item);
    })
}

// 3.join & split
function flatten(arr){
    return arr.join(',').split(',').map(function(item){
        return parseInt(item);
    })
}

// 其它：reduce
         ES6扩展运算符 [].concat(...[1, 2, [3, [4, 5]]]);
```

### 相交链表

找出两个单链表相交的起始节点。

```javascript
// 注意：两个单链表相交不会出现X型交叉，因为单链表每个节点只有一个next指针域
// 如果链表结构中没有循环
// 1.遍历
var getIntersectionNode = function(headA, headB) {
  let p = headA,
    q = headB;
  let arrA = [],
    arrB = [];
  while (p != null) {
    arrA.push(p);
    p = p.next;
  }
  while (q != null) {
    arrB.push(q);
    q = q.next;
  }
  let i = arrA.length - 1,
    j = arrB.length - 1;
  while (i >= 0 && j >= 0) {
    if (arrA[i] !== arrB[j]) {
      return i === arrA.length - 1 ? null : arrA[i + 1];
    } else {
      i--;
      j--;
    }
  }
  return i < 0 ? arrA[0] : arrB[0];
};

// 2.

// 如果链表结构中有循环
```

### [LeetCode](/leetCode/README.md)

## [工作总结](/summary/README.md)
