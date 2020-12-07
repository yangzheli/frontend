## 读书总结

- [JavaScript 高级程序设计](#JavaScript高级程序设计)
- [高性能网站建设进阶指南](#高性能网站建设进阶指南)
- [JavaScript设计模式与开发实践](#JavaScript设计模式与开发实践)
- [Node.js权威指南](#Node.js权威指南)
- [工程数学线性代数 第六版](#工程数学线性代数第六版)

### <<JavaScript 高级程序设计 第 4 版>>

1. JavaScript 与 ECMAScript

- ECMAScript 是 JavaScript 的核心，各个浏览器均以 ECMAScript 作为自己 JavaScript 实现的依据，具体实现各有不同。完整的 JavaScript 包含三个部分：（1）核心（ECMAScript）；（2）文档对象模型（DOM）；（3）浏览器对象模型（BOM）。如下图所示。<br>

  <img src="../assets/JavaScript组成.png" style="width:200px; margin:0 auto">

2. ECMAScript 版本

- ES6/ES2015：新增类、模块、迭代器、生成器、箭头函数、期约、反射、代理和众多新的数据类型；
- ES7：新增 Array.prototype.includes 和指数操作符；
- ES8：新增异步函数（async/await）、SharedArrayBuffer、Atomics API、Object.values()/Object.entries()/Object.getOwnPropertyDescriptors()和字符串填充方法；
- ES9：新增异步迭代、Promise finally()；
- ES10：
- ES11：

3. DOM

- DOM（文档对象模型）：提供与网页内容交互的方法和接口

4. BOM

- BOM（浏览器对象模型）：提供与浏览器交互的方法和接口

5. script 标签

- 将 JavaScript 插入 HTML 的主要方法是使用 script 标签，script 标签共有 8 个属性：async、charset、crossorigin、defer、integrity、language、src 和 type。
- 如果 type 属性值为 module，则代码会被当成 ES6 模块，只有这时候代码中才能出现 import 和 export 关键字；
- script 标签的使用方式有两种：（1）直接在网页中嵌入 JavaScript 代码；（2）在网页中包含外部 JavaScript 文件（更推荐使用外部文件的方式），例如：

```javascript
<script src="example.js"></script>
```

6. ECMAScript 语法

- ECMAScript 中一切都区分大小写，例如，变量 test 和变量 Test 是两个不同的变量；
- 标识符，即变量、函数、属性或函数参数的名称，根据惯例，ECMAScript 标识符使用驼峰大小写的形式，即第一个单词的首字母小写，后面每个单词的首字母大写；
- 严格模式："use strict"。

7. ECMAScript 变量

- ECMAScript 变量是松散类型的，即变量可以保存任何类型的数据，声明变量可以使用 var、let 和 const （let 和 const 为 ES6 新增 ）这 3 个关键字，不同数据类型的变量初始化可以在同一条语句中声明；
- let 声明的是块作用域，var 声明的是函数作用域，例如：

```javascript
if (true) {
  var name = "Tom"; // 函数作用域
  console.log(name); // Tom
}
console.log(name); // Tom
```

```javascript
if (true) {
  let name = "Tom"; // 块作用域
  console.log(name); // Tom
}
console.log(name); // ReferenceError: name未定义
```

- let 在全局作用域中声明的变量不会成为 window 的属性，而 var 声明的变量会；
- 只使用 let 和 const 有助于提高代码质量，const 优先，let 次之。

8. ECMAScript 数据类型

- 6 种简单数据类型/原始类型：Undefined、Null、Boolean、Number、String 和 Symbol（ES6 新增）；
- 1 种复杂数据类型/引用类型：Object/对象。

- typeof 操作符：注意 typeof null 返回"object"；
- Undefined 类型只有一个值即 undefined， 值为 undefined 的变量是 指该变量声明了但未初始化；
- Null 类型也只有一个值即 null，null 值表示一个空对象指针，这就是为什么 typeof null 返回的是"object"；
- Boolean 类型有两个字面值：true 和 false。这两个布尔值不同于数值，即 true 不等于 1，false 不等于 0，但是其他类型的值都能与布尔值进行转换，在 if 等流控制语句中其他类型值会自动转换为布尔值；
- Number 类型
- String 类型
- Symbol 类型：用来确保对象属性使用唯一标识符，不会发生属性冲突。使用 Symbol()函数进行初始化，Symbol()函数不能与 new 关键字一起作为构造函数使用，例如：

```javascript
let n = new Number();
console.log(typeof n); // "object"

let s = new Symbol(); // TypeError: Symbol is not a constructor
```

- Object 类型，Object 是所有对象的基类。

9. ECMAScript 语句

- for-in 语句:一种严格的迭代语句，用于枚举对象中的非符号键属性。由于 ECMAScript 中对象的属性是无序的，因此 for-in 语句不能保证返回对象属性的顺序。

- for-of 语句：一种严格的迭代语句，用于遍历可迭代对象的元素。for-of 循环会按照可迭代对象的 next()方法产生值的顺序迭代元素。ES2018 对 for-of 语句进行了扩展，增加了 for-await-of 循环，以支持生成期约（promise）的异步可迭代对象。示例：

```javascript
// 这里控制语句中的const不是必需的，但为了确保这个局部变量不被修改，推荐使用const
for (const el of [2, 4, 6, 8]) {
  console.log(el);
}
```

10. 原始值与引用值

- 原始值保存在栈内存上，引用值保存在堆内存上；
- 保存原始值的变量是按值访问的，保存引用值的变量是按引用访问的；
- 原始值不能有属性，只有引用值可以动态添加后面可以使用的属性；
- 原始类型的初始化只能使用原始字面量形式，如果使用 new 关键字，会创建一个 Object 类型的实例；
- 通过变量把原始值赋值给另一个变量时，两个变量是完全独立的；

```javascript
let num1 = 5;
let num2 = num1;
```

  <img src="../assets/原始值复制.png" style="width:200px; margin:0 auto">

- 通过变量把引用值赋值给另一个变量时，存储在变量中的值也会被复制到新变量所在的位置，这里复制的实际上是一个指针，它指向存储在堆内存中的对象；

```javascript
let obj1 = new Object();
let obj2 = obj1;
obj1.name = "Tom";
console.log(obj2.name); // "Tom"
```

<img src="../assets/引用值复制.png" style="width:200px; margin:0 auto">

- ECMAScript 所有函数的参数都是按值传递的，ECMAScript 中函数的参数就是局部变量。

11. 变量作用域

- 搜索标识符表示什么过程如下：搜索开始于作用域前端，如果在局部上下文找到该标识符，则搜索停止，变量确定；如果没有找到变量名，则继续沿作用域链搜索。如果搜索到全局上下文，仍然没有找到该标识符，则说明该变量未声明。例如：

```javascript
var color = "blue";
function getColor() {
  let color = "red";
  {
    let color = "green";
    return color;
  }
}

console.log(getColor()); // "green"
```

12. 垃圾回收与内存管理

- JavaScript 是使用垃圾回收的语言，垃圾收集器会定时、周期性地找出不再继续使用的变量，然后释放其占用的内存。标识无用变量的策略通常有两种：<br>
  （1）标记清除（最常用）：垃圾收集器会给内存中所有变量都加上标识，然后去掉环境中的变量和被环境中变量引用的变量的标识，之后仍然被加上标识的变量就会被垃圾收集器回收所占用的内存。<br>
  （2）引用计数：跟踪每个值被引用的次数，当这个值的引用次数变为 0，其占用的内存空间就会被回收。

- 将内存占用量保持在一个较小的值可以让页面性能更好，优化内存占用的最佳手段就是保证在执行代码时只保存必要的数据。如果数据不再必要，就解除引用，比如把它设置为 null；

13. 原始值包装类型

- ECMAScript 提供了 3 种特殊的引用类型：Boolean、Number 和 String。

```javascript
let s1 = "hello world";
let s2 = s1.substring(2); // "llo world"
```

- 在上面的示例中，s1 是一个原始值，从逻辑上讲不应该有方法，实际上后台进行了特殊的处理：<br>
  （1）创建一个 String 包装类型的示例；<br>
  （2）调用实例上的 substring 方法；<br>
  （3）销毁实例。
- 对象的生命周期：通过 new 实例化引用类型后，得到的实例会在离开作用域时被销毁，而自动创建的原始值包装对象只存在于访问它的那行代码执行期间，这就意味着不能给原始值添加属性和方法。
- 使用 new 调用原始值包装类型的构造函数，和调用同名的转型函数并不一样。

```javascript
let value = "25";
let number = Number(value); // 转型函数
console.log(typeof number); // "number"
let obj = new Number(value); // 构造函数，但不推荐显式创建原始值包装类型的示例
console.log(typeof obj); // "object"
```

14. 内置对象

- 除了 Object、Array、Function 和原始值包装对象，ECMAScript 还定义了另外 2 种内置对象：Global 和 Math；
- Global：
- Math：

15. 引用类型

- Object
- Array：数组中每个槽位可以存储任意类型的数据，即可以创建一个数组，它的第一个元素是字符串，第二个元素是数值，第三个元素是对象。ECMAScript 数组是动态大小的，会随着数据添加而自动增长；
- 定型数组
- Map（ES6 新增）：键/值对，与 Object 只能使用数值、字符串和符号作为键不同，Map 可以使用任何 JavaScript 数据类型作为键；
- WeakMap（ES6 新增）：弱映射，WeakMap 中的 “weak” 描述的是 JavaScript 垃圾回收程序对待弱映射中键的方式。弱映射中的键只能是 Object 或继承自 Object 的类型，使用非对象设置键会抛出 TypeError，值类型没有限制；WeakMap 中的键不属于正式的引用，不会阻止垃圾回收；WeakMap 无法对键/值对进行迭代。
- Set（ES6 新增）：一种新的集合类型，Set 可以包含任何 JavaScript 数据类型作为值；
- WeakSet（ES6 新增）：弱集合，WeakSet 中的 “weak” 描述的是 JavaScript 垃圾回收程序对待弱集合中值的方式。弱集合中的值只能是 Object 或继承自 Object 的类型，使用非对象设置键会抛出 TypeError。WeakSet 中的值不属于正式的引用，不会阻止垃圾回收。WeakSet 无法对值进行迭代。
- Function

16. 迭代器

- ES5 新增 Array.prototype.forEach()进行迭代，但 forEach()方法无法标识迭代何时终止；

```javascript
let arr = ["foo", "bar", "app"];
arr.forEach(item => {
  console.log(item);
});
```

- ES6 新增迭代器模式，字符串、数组、Map、Set、arguments 对象和 NodeList 等 DOM 集合类型都实现了 Iterable 接口（可迭代协议）。任何实现 Iterable 接口的对象都有 Symbol.iterator 属性。如果对象原型链上父类实现了 Iterable 接口，那么这个对象也实现了这个接口。通过调用迭代器工厂函数会生成一个迭代器，例如：

```javascript
let str = "abc";
console.log(str[Symbol.iterator]()); // StringIterator {}
```

- 迭代器使用 next()方法在可迭代对象中遍历数据，成功返回的迭代器对象 IteratorResult 包含两个属性：done 和 value。done 是布尔值，表示是否还可以再次调用 next()取下一个值，取 true 是表示“耗尽”，value 包含迭代对象的下一个值。

17. 生成器

- ES6 新增的结构，可以在一个函数块内暂停和恢复代码的执行；

- 生成器的形式是一个函数，函数名称前加一个星号（\*）表示它是一个生成器（标识生成器函数的星号不受两侧空格的影响），箭头函数不能用来定义生成器函数，示例：

```javascript
// 生成器函数声明
function* generatorFn() {}

// 生成器函数表达式
let generatorFn = function*() {};

// 作为对象字面量方法的生成器函数
let foo = {
  *generatorFn() {}
};

// 作为类实例方法的生成器函数
class Foo {
  *generatorFn() {}
}

// 作为类静态方法的生成器函数
class Foo {
  static *generatorFn() {}
}
```

- 调用生成器函数会产生一个生成器对象，生成器对象开始处于暂停执行（suspended）状态，生成器对象也实现了 Iterator 接口，具有 next()方法，调用 next()方法会让生成器开始或恢复执行；

- yield 关键字可以让生成器停止和开始执行，生成器函数在遇到 yield 之前会正常执行，遇到 yield 之后执行会停止，函数作用域的状态会被保留，只能通过调用 next()方法来恢复执行；

- yield 关键字只能在生成器函数内部使用，出现在嵌套的非生成器函数中会抛出语法错误；

18. 对象

- ECMAScript 将对象定义为一组属性的无序集合，对象的每个属性和方法都由一个名称标识，这个名称映射到一个值，可以把 ECMAScript 中的对象想象为一张散列表，其中内容就是名/值对，值可以是数据或函数；

- 对象的属性分为两种：数据属性和访问器属性。

- 数据属性有 4 个特性描述它们的行为：[[Configurable]]、[[Enumerable]]、[[Writable]]和[[Value]]，要修改属性的默认特征，必须使用 Object.defineProperty()方法，示例：

```javascript
let person = {};
Object.defineProperty(person, "name", {
  writable: false, // 只读
  value: "Nicholas"
});
console.log(person.name); // "Nicholas"
person.name = "Greg";
console.log(person.name); // "Nicholas"
```

- 虽然对于同一属性可以多次调用 Object.defineProperty()，但在 configurable 值设为 false 后再次调用就会报错。同时在调用 Object.defineProperty()时，configurable、enumerable 和 writable 的值如果不指定，就默认为 false；

- 访问器属性不包含数据值，有 4 个特性描述它们的行为：[[Configurable]]、[[Enumerable]]、[[Get]]和[[Set]]，访问器属性是不能直接定义的，必须使用 Object.defineProperty()；

- 可以通过 Object.defineProperties()方法一次性定义多个属性；

- 可以使用 Object.getOwnPropertyDescriptor()和 Object.getOwnPropertyDescriptors()（ES7 新增）方法读取属性的特性；

- ES6 新增 Object.assign()方法用来合并对象，该方法接受一个目标对象和一个或多个源对象作为参数，然后将每个源对象中的可枚举（Object.propertyIsEnumerable()返回 true）和只有（Object.hasOwnProperty()返回 true）属性复制到目标对象。如果多个源对象都有相同的属性，则使用最后一个复制的值。示例：

```javascript
let dest = {},
  a = { id: "a" },
  b = { id: "b" };
// 浅拷贝
let res = Object.assign(dest, a, b);
console.log(res === dest); // true
```

- 对象相等判定：ES6 之前使用 === 操作符进行判断，但有些特殊情况 === 无能为力，因此，ES6 新增 Object.is()方法来判定对象是否相等。

- 增强的对象语法

- 对象解构：涉及多个属性的解构赋值是一个输出无关的顺序化操作，如果一个解构表达式涉及多个赋值，开始的赋值成功而后面的赋值出错，则整个解构赋值只会完成一部分。

19. 创建对象

- Object 构造函数；

- 对象字面量；

- 工厂模式：按照特定接口创建对象的方式，虽然可以解决创建多个类似对象的问题，但没有解决对象标识问题（即新创建的对象是什么类型）。例如：

```javascript
function createPerson(name, age, job) {
  let o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function() {
    console.log(this.name);
  };
  return o;
}

let p1 = createPerson("Nicholas", 20, "Doctor");
```

- 构造函数模式：用于创建特定类型对象。例如：

```javascript
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function() {
    console.log(this.name);
  };
}

let p1 = new Person("Nicholas", 20, "Doctor");
```

Person() 构造函数与 createPerson() 工厂函数有如下区别：<br>
（1）没有显示创建对象；<br>
（2）属性和方法直接赋值给 this；<br>
（3）函数没有 return。<br>
同时构造函数名称的首字母都是大写的，非构造函数则以小写字母开头。

使用 new 操作符调用构造函数会执行以下操作：<br>
（1）在内存中创建一个新对象；<br>
（2）新对象的[[Prototype]]特性被赋值为构造函数的 prototype 属性；<br>
（3）构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）；<br>
（4）执行构造函数内部的代码（给新对象添加属性）；<br>
（5）如果构造函数返回非空对象，则返回该对象，否则返回刚创建的新对象。

构造函数和普通函数唯一的区别就是调用方式不同，任何函数只要使用 new 操作符调用就是构造函数，而不使用 new 操作符调用的函数就是普通函数。前面定义的 Person()也可以像下面这样调用：

```javascript
// 作为函数调用
Person("Greg", 25, "Engineer");
window.sayName(); // "Greg"

// 在另一个对象的作用域中调用
let obj = new Object();
Person.call(obj, "Jerry", 30, "Nurse");
o.sayName(); // "Jerry"
```

在上面的例子中，没有使用 new 操作符调用 Person()，会将属性和方法添加到 window 对象。注意，在调用一个函数而没有明确设置 this 的情况（即没有作为对象的方法调用，也没有使用 call()/apply()调用），this 始终指向 Global 对象（在浏览器中就是 window 对象）。

构造函数有一个问题就是：其中定义的方法会在每个实例上都创建一遍，而如果将方法定义在构造函数外部，那个函数实际上只能在一个对象上调用。可以通过原型模式来解决。

- 原型模式：每个函数都会创建一个 prototype 属性，这个属性是一个对象，这个对象就是构造函数的原型，在它上面定义的方法和属性可以被对象实例共享。示例：

```javascript
function Person() {}

Person.prototype.name = "Nicholas";
Person.prototype.age = 20;
Person.prototype.jog = "Doctor";
Person.sayName = function() {
  console.log(this.name);
};

let p1 = new Person(),
  p2 = new Person();
console.log(p1.sayName == p2.sayName); // true
```

20. 原型

- 原型：实例与构造函数原型之间有直接的联系，但实例与构造函数之间没有。

<img src="../assets/原型链.png" style="width:250px; margin:0 auto">

- 原型层级：在通过对象访问属性时，会按照这个属性的名称进行搜索。搜索开始于对象实例本身。如果在这个实例上发现了给定的名称，则返回该名称对应的值。如果没有找到这个属性，就会沿着指针进入原型对象，然后在原型对象上找到属性后，再返回相应的值。<br>
  hasOwnProperty()方法可以用于确定某个属性是在实例上还是原型对象上。

- 其他原型语法：直接通过一个包含所有属性和方法的对象字面量来重写原型。示例：

```javascript
function Person() {}

Person.prototype = {
  name: "Nicholas",
  age: 20,
  job: "doctor",
  sayName() {
    console.log(this.name);
  }
};
```

这样重写之后，只有一个问题就是：Person.prototype 的 constructor 属性就不指向 Person 了。因为在创建函数时，也会创建它的 prototype 对象，同时会自动给这个原型的 constructor 属性赋值。上面的写法完全重写了默认的 prototype 对象，因此其 constructor 属性也指向了完全不同的新对象（Object 构造函数）。可以像下面一样在重写原型对象时专门设置一下它的值：

```javascript
function Person() {}

Person.prototype = {
  constructor: Person,
  name: "Nicholas",
  age: 20,
  job: "doctor",
  sayName() {
    console.log(this.name);
  }
};
```

- 原生对象原型：是实现所有原生引用类型的模式，所有原生引用类型的构造函数（包括 Object、Array、String 等）都在原型上定义了实例方法。例如数组实例的 sort()方法就是在 Array.prototype 上定义的。虽然可以像修改自定义对象原型一样修改原生对象类型，但不推挤这样做，推荐的做法是创建一个自定义的类，继承原生类型。

- 原型模式的问题：共享特性，由于原型上所有的属性是在实例间共享的，但一般来说，不同的实例应该有属于自己的属性副本，这就是实际开放中通常不单独使用原型模式的原因。

21. 对象迭代

- ES2017 新增了两个静态方法 Object.values()和 Object.entries()，用于将对象内容转化为序列化的、可迭代的格式，返回它们内容的数组。Object.values()返回对象值的数组，Object.entries()返回键/值对的数组（非字符串属性会被转换为字符串输出）。

22. 继承

- 很多面向对象语言都支持两种继承：接口继承和实现继承。接口继承只继承方法签名，实现继承继承实际的方法。由于 ECMAScript 中函数没有签名，因此接口继承在 ECMAScript 中是不可能的，实现继承是 ECMAScript 唯一支持的继承方式，而这主要通过原型链实现。实现继承的方式有：<br>
  （1）原型链；
  （2）盗用构造函数；
  （3）组合继承；

23. 原型链

- 原型链：每个构造函数都有一个原型对象，原型有一个 constructor 属性指向构造函数，而实例有一个内部指针指向原型。如果原型是另一个类型的实例，就意味着这个原型本身有一个内部指针指向另一个原型，相应地另一个原型也有一个指针指向另一个构造函数。这样就在实例和原型之间构成了一条原型链。示例：

```javascript
function SuperType() {}

function SubType() {}

// 实现继承
SubType.prototype = new SuperType();
```

- 默认原型：默认情况下，所有引用类型都继承自 Object，这也是通过原型链实现的。任何函数的默认原型都是 Object 的一个实例，这也是自定义类型能够继承包括 toString()、valueOf()在内所有默认方法的原因。

- 原型和继承关系：原型和实例的关系可以通过两种方式来确定，<br>
  （1）使用 instanceof 操作符；<br>
  （2）使用 isPrototypeOf()方法，原型链中每个原型都可以调用这个方法，例如：

```javascript
console.log(Object.isPrototypeOf(instance)); // true
console.log(SuperType.isPrototypeOf(instance)); // true
```

- 关于方法：子类有时候需要覆盖父类的方法，或者增加父类没有的方法。这些方法必须在原型赋值之后再添加到原型上。示例：

```javascript
function SuperType() {
  this.property = true;
}

SuperType.prototype.getSuperValue = function() {
  return this.property;
};

function SubType() {
  this.subProperty = false;
}

// 继承
SubType.prototype = new SuperType();

// 覆盖已有方法
SubType.prototype.getSuperValue = function() {
  return false;
};

// 新方法
SubType.prototype.getSubValue = function() {
  return this.subProperty;
};
```

- 以对象字面量方式创建原型方法会破坏之前的原型链，因为这相当于重写了原型链。示例：

```javascript
function SuperType() {}

SuperType.prototype.getSuperValue = function() {
  return true;
};


function SubType() {}

// 继承
SubType.prototype = new SuperType();
// 覆盖后的原型是Object的实例，不再是SuperType的实例，因此SubType与SuperType之间就没有关系了
SubType.prototype={
  getSubValue(){
    return false;
  }
  otherMethod(){
    return false;
  }
}

let instance = new SubType();
console.log(instance.getSuperValue());  // 报错！
```

- 原型链的问题：（1）共享特性，原型中的引用值会在所有实例间共享，这也是为什么属性通常会在构造函数中定义而不会定义在原型上的原因。<br>
  （2）子类型在实例化时不能给父类型的构造函数传参。<br>
  因此，原型链基本不会被单独使用。<br>
  示例：

```javascript
function SuperType() {
  this.colors = ["red", "blue", "white"];
}

function SubType() {}

SubType.prototype = new SuperType();

let instance1 = new SubType();
instance1.colors.push("black");

let instance2 = new SubType();
console.log(instance2.colors); //"red", "blue", "white","black"
```

24. 盗用构造函数

- 为解决原型包含引用值导致的继承问题，“盗用构造函数”的技术流行起来。思路：在子类构造函数中调用父类构造函数。因为函数是在特定上下文中执行代码的简单对象，所以可以使用 call()、apply()方法以新创建的对象为上下文执行构造函数。示例：

```javascript
function SuperType() {
  this.colors = ["red", "green", "blue"];
}

function SubType() {
  SuperType.call(this);
}

let instance1 = new SubType();
instance1.colors.push("black");
console.log(instance1.colors);

let instance2 = new SubType();
console.log(instance2.colors);
```

- 优点：可以在子类构造函数中向父类构造函数传递参数。示例：

```javascript
function SuperType(name) {
  this.name = name;
}

function SubType() {
  // 继承SuperType并传参
  SuperType.call(this, "Nicholas");

  this.age = 20;
}
```

- 盗用构造函数的问题：必须在构造函数中定义方法，因此函数不能重用。而且子类也不能访问父类原型上定义的方法。因此，盗用构造函数基本上也不单独使用。

25. 组合继承

- 组合继承（伪经典继承）综合了原型链和盗用构造函数。思路：使用原型链继承原型上的属性和方法，而通过盗用构造函数继承实例属性。组合继承是 JavaScript 中使用最多的继承模式，示例：

```javascript
function SuperType(name) {
  this.name = name;
  this.colors = ["red", "green", "blue"];
}
SuperType.prototype.sayName = function() {
  console.log(this.name);
};

function SubType(name, age) {
  // 继承属性
  SuperType.call(this, name);

  this.age = age;
}

// 继承方法
SubType.prototype = new SuperType();

SubType.prototype.sayAge = function() {
  console.log(this.age);
};

let instance1 = new SubType("Nicholas", 20);
instance1.colors.push("white");
console.log(instance1.colors);

let instance2 = new SubType();
console.log(instance2.colors);
```

26. 原型式继承

- 通过下面的 object()方法对传入的对象执行浅复制。

```javascript
function object(o) {
  function F() {}
  F.prototpe = o;
  return new F();
}
```

- ES5 新增 Object.create()方法将原型式继承规范化，方法接收两个参数：作为新对象原型的对象，以及给新对象定义额外属性的对象（可选）。在只有一个参数时，Object.create()和上面的 object()方法效果相同。

- 原型式继承属性中包含的引用值始终会在相关对象间共享。

27. 寄生式继承

- 寄生式继承背后思路类似于寄生构造函数和工厂模式，具体思路：创建一个实现继承的函数，以某种方式增强对象，然后返回这个对象。

```javascript
// object函数不是寄生式继承必需的，任何返回新对象的函数都能在这里使用
function createAnother(original) {
  let clone = object(original); // 通过调用object函数创建一个新对象
  clone.sayHi = function() {
    // 以某种方式增强这个对象
    console.log("Hi");
  };
  return clone; // 返回这个对象
}
```

使用示例：

```javascript
let person = {
  name: "Nicholas",
  friends: ["Nick", "Van"]
};

let anotherPerson = createAnother(person);
anotherPerson.sayHi(); // "Hi"
```

- 缺点：与构造函数模式类似，寄生式继承给对象添加函数会导致函数难以重用。

28. 寄生式组合继承

- 寄生式组合继承：通过盗用构造函数继承属性，但使用混合式原型继承方法。

```javascript
function inheritPrototype(subType, superType) {
  let prototype = object(superType.prototype); // 创建对象
  prototype.constructor = subType; // 增强对象
  subType.prototype = prototype; // 赋值对象
}
```

使用实例：

```javascript
function SuperType(name) {
  this.name = name;
  this.colors = ["red", "green", "white"];
}

SuperType.prototype.sayName = function() {
  console.log(this.name);
};

function SubType(name, age) {
  SuperType.call(this, name);
  this.age = age;
}

inheritPrototype(SubType, SuperType);
SubType.prototype.sayAge = function() {
  console.log(this.age);
};
```

- 寄生式组合继承算是引用类型继承的最佳模式。

29. 类

- 前面通过只使用 ES5 的特性来模拟类似于类的行为，ES6 新引入的 class 关键字具有正式定义类的能力。类（class）是 ECMAScript 中新的基础性语法糖结构，实际上背后使用的仍然是原型和构造函数的概念。

- 类的定义：与函数类型相似，定义类也主要有两种方式：类声明和类表达式。

```javascript
// 类声明
class Person {}

// 类表达式
const Person = class {};
```

与函数表达式类似，类表达式在它们被求值前也不能引用。不过，与函数定义不同的是，虽然函数声明可以提升，但类定义不能。同时，函数受函数作用域限制，而类受块作用域限制。实例：

```javascript
console.log(FunctionExpression); // undefined
var FunctionExpression = function() {};
console.log(FunctionExpression); // ƒ () {}

console.log(FunctionDeclaration); // FunctionDeclaration() {}

function FunctionDeclaration() {}
console.log(FunctionDeclaration); // FunctionDeclaration() {}

console.log(ClassExpression); // undefined
var ClassExpression = class {};
console.log(ClassExpression); // class {}

console.log(ClassDeclaration); // ReferenceError
class ClassDeclaration {}
console.log(ClassDeclaration); // class ClassDeclaration {}
```

- 类的构成：类可以包含构造函数方法、实例方法、获取函数、设置函数和静态类方法。但这些都不是必需的，空的类定义同样有效。

- 类构造函数：constructor 关键字。使用 new 操作符创建类的新实例时，会调用这个方法。具体分为以下几步：<br>
  （1）在内存中创建一个新对象；<br>
  （2）这个新对象的[[Prototype]]指针被赋值为构造函数的 prototype 属性；<br>
  （3）构造函数内部的 this 被赋值为这个新对象（即 this 指向新对象）；<br>
  （4）执行构造函数内部的代码（给新对象添加属性）；<br>
  （5）如果构造函数返回非空对象，则返回该对象；否则返回刚创建的新对象。

```javascript
class Person {
  constructor(override) {
    this.foo = "foo";
    if (override) {
      return {
        bar: "bar"
      };
    }
  }
}

let p1 = new Person(),
  p2 = new Person(true);

console.log(p1); // Person{foo:"foo"}
console.log(p1 instanceof Person); // true

console.log(p2); // Object{bar:"bar"}
console.log(p2 instanceof Person); // false
```

- 类构造函数和构造函数的主要区别：调用类构造函数必须使用 new 操作符，而普通构造函数如果不适用 new 调用，那么就会以全局的 this（通常是 window）作为内部对象。

```javascript
function Person() {}

class Animal {}

// 把window作为this来创建实例
let p = Person();

let a = Animal(); // TypeError
```

- 类本身具有和普通构造函数一样的行为，类本身在使用 new 调用时就会被当成构造函数。

- ES6 类支持单继承。使用 extends 关键字，就可以继承任何具有[[Construct]]和原型的对象，这意味着不仅可以继承一个类，也可以继承普通的构造函数。

- 继承：

30. 代理与反射

- 代理：代理是目标对象的抽象，它可以用作目标对象的替身，又完全独立于目标对象。目标对象既可以直接被操作，也可以通过代理来操作。但直接操作会绕过代理施予的行为。

- 代理是使用 Proxy 构造函数创建的，这个构造函数接收两个参数：目标对象和处理程序对象。缺少任何一个参数都会抛出 TypeError。

- 空代理：除了作为一个抽象的目标对象，什么也不做。要创建空代理，可以传一个简单的对象字面量作为处理程序对象。例如：

```javascript
const target = {
  id: "target"
};
const handler = {};
const proxy = new Proxy(target, handler);
console.log(target.id);
console.log(proxy.id);
```

- 捕获器：捕获器是在处理程序对象中定义的“基本操作的拦截器”。每个捕获器对应一个基本操作，在代理对象上调用这些基本操作时，代理可以在这些操作传播到目标对象前先调用捕获器函数，拦截并修改相应的行为。例如定义一个 get()捕获器：

```javascript
const target = {
  id: "target"
};
const handler = {
  // 捕获器在处理程序对象中以方法名为键
  get() {
    return "handler";
  }
};
const proxy = new Proxy(target, handler);

console.log(target.id);
console.log(proxy.id);
```

- 处理程序对象中所有可以捕获的方法都有对应的（Reflect）API 方法，这些方法和捕获器拦截的方法具有相同的名称和函数签名，而且也具有与被拦截方法相同的行为。例如用反射 API 像下面这样定义空代理对象：

```javascript
const target = {
  id: "target"
};
const handler = {
  get() {
    return Reflect.get(...arguments);
  }
};
const proxy = new Proxy(target, handler);

console.log(target.id);
console.log(proxy.id);
```

- 状态标记：很多反射方法返回称作“状态标记”的布尔值，表示执行的操作是否成功。例如：

```javascript
// 初始代码
const o ={};
try{
  Object.defineProperty(o,'foo','bar');
  console.log('success');
}else{
  console.log('failure');
}
```

```javascript
// 重构后的代码
const o = {};
if (Reflect.defineProperty(o, "foo", { value: "bar" })) {
  console.log("success");
} else {
  console.log("failure");
}
```

- 多层拦截：代理可以拦截反射 API 的操作，这意味着可以创建另一个代理，通过它去代理另一个代理，这样就可以在目标对象构建多层拦截网。

```javascript
const target = {
  id: "target"
};
const firstProxy = new Proxy(target, {
  get() {
    console.log("first proxy");
    return Reflect.get(...arguments);
  }
});
const secondProxy = new Proxy(target, {
  get() {
    console.log("second proxy");
    return Reflect.get(...arguments);
  }
});
```

- 代理的问题：（1）代理中的 this；（2）代理与内部槽位。

- 代理模式：（1）跟踪属性访问：通过捕获 get、set 和 has 等操作，可以知道对象属性什么时候被访问；<br>
  （2）隐藏属性：代理内部的实现对外部代码是不可见的，可以轻易的隐藏目标对象上的属性；<br>
  （3）属性验证：由于所有赋值操作都会触发 set()捕获器，所以可以根据所赋的值决定是允许还是拒绝赋值；<br>
  （4）函数与构造函数参数验证；<br>
  （5）数据绑定与可观察对象；

31. 函数

- 函数实际上是对象，每个函数都是 Function 类型的实例。因为函数是对象，函数名就是指向函数对象的指针。

- 函数定义方式有：函数声明，函数表达式，箭头函数，Funtion 构造函数。示例：

```javascript
// 函数声明
function sum(num1, num2) {
  return num1 + num2;
}

// 函数表达式
let sum = function(num1, num2) {
  return num1 + num2;
};

// 箭头函数
let sum = (num1, num2) => {
  return num1 + num2;
};

// Function 构造函数（不推荐）
let sum = new Function("num1", "num2", "return num1 + num2");
```

- 箭头函数：ES6 新增(=>)定义函数表达式的能力，箭头函数实例化函数对象与正式的函数表达式创建函数的行为是相同的，任何可以使用函数表达式的地方，都可以使用箭头函数。

- 函数名就是指向函数的指针，所以它们跟其它包含对象指针的变量具有相同的行为，这意味着一个函数可以有多个名称。示例：

```javascript
function sum(num1, num2) {
  return num1 + num2;
}
console.log(sum(18, 12)); // 30

let anotherSum = sum;
console.log(anotherSum(18, 12)); // 30

sum = null;
console.log(anotherSum(18, 12)); // 30
```

注意：使用不带括号的函数名会访问函数指针，而不会执行函数。

- 函数参数：ECMAScript 函数的参数跟大多数其他语言不同，ECMAScript 函数既不关心传入的参数个数，也不关心这些参数的数据类型。主要是因为 ECMAScript 函数的参数在内部表现为一个数组，函数被调用时总会接收一个数组，但函数并不关心这个数组包含什么。事实上，使用 function 关键字定义函数时，可以在函数内部访问 arguments 对象，从中取得传进来的每个参数值。<br>
  ECMAScript 函数的参数只是为了方便才写出来的，并不是必须写出来的，ECMAScript 根本不存在验证命名参数的机制。<br>
  arguments 对象可以和函数命名参数一起使用。

- 箭头函数的参数：如果函数是使用箭头语法定义的，那么传给函数的参数将不能使用 arguments 关键字访问，只能通过定义的命名参数访问。

- ECMAScript 中所有参数都是按值传递的，不可能按引用传递参数。如果把对象作为参数传递，那么传递的值就是这个对象的引用。

- ECMAScript 中函数是没有重载的，如果定义了两个同名函数，那么后定义的会覆盖先定义的。

- 函数声明提升：JavaScript 引擎在任何代码执行之前，会先读取函数声明，并在执行上下文中生成函数定义。而函数表达式必须等到代码执行到它那一行，才会在执行上下文生成函数定义。示例：

```javascript
console.log(add(12, 8));

function add(num1, num2) {
  return num1 + num2;
}

// TypeError
console.log(mul(3, 4));
var mul = function(num1, num2) {
  return num1 * num2;
};
```
除了函数在什么时候有定义外，函数声明和函数表达式是等价的。

- 函数属性和方法：ECMAScript中的函数都是对象，因此有属性和方法。每个函数都有两个属性：length和prototype。length属性保存函数定义的命名参数的个数，prototype属性保存引用类型所有实例方法，这意味着toString()、valueOf()等方法实际上都保存在prototype上。

- 函数表达式的不同形式：
```javascript
let functionName = function(arge){
  // 函数体
}
```
这样创建的函数叫匿名函数，因为function关键字后面没有标识符，未赋值给其他变量的匿名函数的name属性是空字符串。

- 尾调用优化：ES6新增了一项内存管理优化机制，让JavaScript引擎在满足条件时可以重用栈帧。尾递归优化的条件就是确定外部栈帧真的没有必要存在了：<br>
（1）代码在严格模式下执行；<br>
（2）外部函数的返回值是对尾调用函数的调用；<br>
（3）尾调用函数返回后不需要执行额外的逻辑；<br>
（4）尾调用函数不是引用外部函数作用域中自由变量的闭包。

- 立即调用的函数表达式（IIFE）：使用IIFE可以模拟块级作用域，即在一个函数表达式内部声明变量，然后立即执行这个函数。
```javascript
(function(){
  // 块作用域
})();
```

32. 扩展运算符

- 扩展运算符(...)：ES6 新增，使用扩展运算符可以简洁地操作和组合集合数据。扩展运算符最有用的场景就是函数定义中的参数列表，既可以用于调用函数时传参，也可以用于定义函数参数。示例：

```javascript
function add() {
  let sum = 0;
  for (let i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }
  return sum;
}

let arr = [1, 2, 3, 4];
console.log(add.apply(null, arr)); // 10
// 可以用来替代apply方法
console.log(add(...arr)); // 10
```

33. 期约（Promise）

34. 异步函数

### 《高性能网站建设进阶指南》

1. Ajax 性能

- 权衡：权衡时间、质量和成本
- 优化原则：重点放在对程序整体开销影响最大的部分
- 浏览器：浏览器通常在运行 JavaScript 上花费的时间很少，绝大部分时间消耗在 DOM 上

2. 快速响应的 Web 程序

- 怎样才算足够快：<br>
  （1）0.1 秒：如果 JavaScript 代码执行时间超过 0.1 秒，页面将会给人感觉不够平滑快捷；<br>
  （2）1 秒：如果执行时间超过 1 秒，则会给人感觉缓慢；<br>
  （3）10 秒：超过 10 秒，用户将非常沮丧。

- 测量延迟时间：手动代码检测或自动代码检测（例如 Firefox 的流行插件 Firebug）

- JavaScript 是单线程的

- Web Workers、Gears：允许浏览器的主 JavaScript 线程创建后台的“Worker”，在这些 Worker 启用时从浏览器线程中接收到一些简单的信息（如独立状态，而不是对共享变量的引用），并在完成时返回一条信息

- 使用定时器：将运行时间很长的运算拆分成独立的区块，使用定时器控制其执行

- XMLHttpRequest（XML）：有异步模式

- 内存管理：JavaScript 实现了垃圾回收（garbage collection，简称“GC”）。当然，自动内存管理是有开销的。当执行垃圾回收时，垃圾收集器为完成其工作，需要在一段时间内防止所有其他线程（包括正在调用的主浏览器 JavaScript 线程）访问它正在处理的堆空间，直到遍历完整个创建对象的“堆”（当然，这种暂停通常很短，很难察觉到）。在这个过程中，查找那些不再使用或能够回收未用内存的对象。

3. 拆分初始化负载

- 动态加载：Ajax 和 DHTML（动态 HTML）普及使得如今网站上的 JavaScript 和 CSS 比以往要多，很大一部分应用代码不会在启动时被使用，因此可以采用动态加载的方式。

- 延迟下载：初始化页面时，直到触发 onload 事件，大部分函数并未执行，如果延迟下载这些未执行的函数，初始化时 JavaScript 的下载量将大大减少。以 onload 事件为截止点，因为之后这些功能也应该在页面渲染完成时开始加载。

- 拆分 JavaScript 代码：<br>
  （1）Firebug 的 JavaScript 性能分析器可以显示在触发 onload 事件之前所有已执行的函数名，通过这个可以将 JavaScript 代码拆分为两个文件：一个用于初始化，另一个则可以延迟加载。当然，一些函数虽然没被使用，但仍然是必需的，如错误处理和一些条件判断代码。<br>
  （2）使用微软开发的自动拆分 JavaScript 系统——Doloto。

- 未定义标识符处理：<br>
  在延迟加载的代码与用户页面元素相关联的情况：<br>
  （1）通过改变元素的展现，如包含一个“加载中...”的图标；<br>
  （2）在延迟加载的代码里绑定界面元素的事件处理程序。<br>
  在延迟加载的代码不与用户页面元素相关联的情况：<br>
  使用桩（stub）函数，桩函数是一个与原函数名称相同，但函数体为空、或用一些临时代码代替原有内容的函数，当 JavaScript 代码下载完成后，原函数将覆盖桩函数。例如桩函数返回一个空字符串，用户在完整函数下载完成之前使用将没有任何反应。

- 同样也可以对 CSS 样式表进行拆分，但节省的资源要相对少一些。

4. 无阻塞加载脚本

- 脚本阻塞并行下载<br>
  JavaScript 以行内脚本或外部脚本的形式包含在网页中。行内脚本通过 script 标签引入整段 JavaScript 代码，外部脚本通过 script 的 src 属性把独立文件中的 JavaScript 引入。<br>
  通常浏览器是并行下载的，但对于外部脚本并非如此。当浏览器下载外部脚本时，在脚本下载、解析并执行完毕之前，不会下载任何其他内容。<br>
  浏览器在下载和执行脚本时出现阻塞，是因为浏览器要确保脚本按它们在 HTML 文档中出现的顺序来执行，因为它们之间可能有依赖关系。<br>
  很显然脚本必须按顺序执行，但没有必要按顺序下载。

- 引用外部脚本时避免阻塞方法：XHR Eval、XHR 注入、Script in iframe、Script DOM Element、Script Defer、document.write.Script Tags。但是由于脚本是并行下载的，会导致它们会按它们下载完成的顺序执行，而不是按照它们在 HTML 文档中的顺序。因此这可能会导致竞争状态，惊醒导致未定义标识符错误。

5. 整合异步脚本

### 《JavaScript 设计模式与开发实践》

1. 静态类型语言与动态类型语言

- 编程语言按照数据类型可以分为两类：静态类型语言和动态类型语言。
- 静态类型语言在编译时就已确定变量的类型，而动态类型语言的变量类型要到程序运行的时候，待变量被赋予某个值时后，才会具有某种类型。

2. 多态

- 多态：给不同的对象发送同一个消息时，这些对象会根据这个消息分别给出不同的反馈。
- 示例：

```javascript
let makeSound = function(animal) {
  if (animal instanceof Duck) {
    console.log("嘎嘎嘎");
  } else if (animal instanceof Chicken) {
    console.log("咯咯咯");
  }
};

let Duck = function() {};
let Chicken = function() {};

makeSound(new Duck()); //  "嘎嘎嘎"
maekSound(new Chicken()); // "咯咯咯"
```

- 通过把不变的部分隔离出来，把可变的部分封装起来。让程序具有可扩展性，也符合开放-封闭原则。封装后的示例：

```javascript
let makeSound = function(animal) {
  animal.sound();
};

let Duck = function() {};
Duck.prototype.sound = function() {
  console.log("嘎嘎嘎");
};

let Chicken = function() {};
Chicken.prototype.sound = function() {
  console.log("咯咯咯");
};

makeSound(new Duck()); //  "嘎嘎嘎"
maekSound(new Chicken()); // "咯咯咯"
```

- 类型检查是表现出对象多态性之前绕不开的话题。以静态类型语言 Java 为例，可以通过使用继承，将对象向上转型，得到多态效果。而由于 JavaScript 是不必进行类型检查的动态语言，这就意味着 JavaScript 对象的多态性是与生俱来的。

3. 封装

- 封装：封装目的是将信息隐藏，广义的封装不仅包括封装数据和封装实现，还包括封装类型和封装变化。从设计模式的角度出发，封装更重要的层面体现为封装变化。

- 封装变化：把程序中变化的部分封装好之后，剩下的即是稳定而可复用的部分。

4. 原型模式

- 原型模式是一种设计模式，更是一种编程范式。

- 原型模式是用于创建对象的一种模式，原型模式是通过克隆来创建对象的。ES5 提供了 Object.create()方法用来克隆对象。

- 要得到一个对象，不是通过实例化类，而是找到一个对象作为原型并克隆它。如果对象无法响应某个请求，它会把这个请求委托给它的构造器的原型。

- 基于原型链委托机制是原型继承的本质。

- JavaScript 中，虽然每个对象都是从 Object.prototype 中克隆出来的，但对象构造器的原型并不仅限于 Object.prototype，还可以动态的指向其它对象。

- null 是原型链的终点。

5. this

- JavaScript 中的 this 总是指向一个对象，具体指向哪个对象是在基于函数的执行环境动态绑定的，而非函数被声明时的环境。<br>
  除去 with 和 eval 的情况，this 的指向大致可以分为以下 4 种：<br>
  （1）作为对象的方法调用；<br>
  （2）作为普通函数调用；<br>
  （3）构造器调用；<br>
  （4）Function.prototype.call 或 Function.prototype.apply 调用；

- 作为对象的方法调用：当函数作为对象的方法被调用时，this 指向该对象。示例：

```javascript
let obj = {
  age: 20,
  getAge: function() {
    console.log(this === obj); // true
    console.log(this.age); //20
  }
};

obj.getAge();
```

- 作为普通函数调用：当函数不作为对象的属性被调用时，即作为普通函数被调用，此时的 this 总是指向全局对象。在浏览器的 JavaScript 中，这个全局对象就是 window 对象。示例：

```javascript
window.name = "globalName";

let getName = function() {
  return this.name;
};

console.log(getName()); // "globalName"
```

```javascript
window.name = "globalName";
let myObject = {
  name: "Jerry",
  getName: function() {
    return this.name;
  }
};

console.log(myObject.getName()); // "Jerry"
let getName = myObject.getName;
console.log(getName()); // "globalName"
```

在 div 节点的事件函数内部，有一个局部的 callback 方法，callback 被作为普通函数调用时，callback 的 this 指向了 window。

```javascript
<html>
  <body>
    <div id="div1">hello world</div>
    <script>
      window.id = "window";
      document.getElementById("div1").onclick = function (){
        console.log(this.id); // "div1"
        let callback = function () {
          console.log(this.id); // "window"
        }
        callback();
      }
    </script>
  </body>
</html>
```

往往我们想让它指向该 div 节点，可以用一个变量保存该 div 节点的引用。

```javascript
document.getElementById("div1").onclick = function() {
  let that = this;
  let callback = function() {
    console.log(that.id);
  };
  callback();
};
```

- 构造器调用：当用 new 运算符调用函数时，该函数总是返回一个对象，通常情况下，构造器里的 this 就指向返回的这个对象。示例：

```javascript
let MyClass = function() {
  this.name = "Jerry";
};
let obj = new MyClass();
console.log(obj.name); // "Jerry"
```

但是需要注意，用 new 调用构造器时，如果构造器显式返回一个 Object 类型的对象，那么此次运算结果最终会返回这个对象，而不是之前的 this。示例：

```javascript
let MyClass = function() {
  this.name = "Jerry";
  return {
    // 显式返回一个对象
    name: "Tom"
  };
};
let obj = new MyClass();
console.log(obj.name); // "Tom"
```

如果构造器不显示返回任何数据，或者返回的是一个非对象类型的数据，就不会造成上述问题。示例：

```javascript
let MyClass = function() {
  this.name = "Jerry";
  return "Tom"; // 返回String类型
};
let obj = new MyClass();
console.log(obj.name); // "Jerry"
```

- Function.prototype.call 或 Function.prototype.apply 调用:call 和 apply 可以动态地改变传入函数的 this。示例：

```javascript
let obj1 = {
  name: "Jerry",
  getName: function() {
    return this.name;
  }
};
let obj2 = {
  name: "Tom"
};
console.log(obj1.getName()); // "Jerry"
console.log(obj1.getName.call(obj2)); // "Tom"
```

6. call 和 apply

- call 和 apply 的作用一摸一样，区别仅在于传入参数的形式不同。<br>
  apply 接受两个参数，第一个参数指定了函数内 this 对象的指向，第二个参数为一个带下标的集合，把集合中的元素作为参数传递给被调用的函数。<br>
  call 传入的参数不固定，第一个参数也是代表函数体内的 this 指向，从第二个参数往后，每个参数被依次传入函数。示例：

```javascript
let func = function(a, b, c) {
  console.log([a, b, c]); // [1, 2, 3]
};
func.apply(null, [1, 2, 3]);
func.call(null, 1, 2, 3);
```

- JavaScript 的参数在内部就是用一个数组来表示的，从这个意义上来说，apply 比 call 的使用率更高。

- 当使用 call 和 apply 的时候，如果传入的第一个参数为 null，函数体内的 this 会指向默认的宿主对象，在浏览器中则是 window。但如果在严格模式下，函数体内的 this 还是为 null。

- 有时候使用 call 和 apply 的目的不在于指定 this 指向，而是另有用途，比如借用其他对象的方法，可以传入 null 代替某个具体的对象。示例：

```javascript
Math.max.apply(null, [1, 2, 3, 1, 4, 5]); // 5
```

- call 和 apply 的用途：<br>
  （1）改变 this 指向；<br>
  （2）Function.prototype.bind；<br>
  （3）借用其他对象的方法。<br>

- 简化版的 Function.prototype.bind 实现：

```javascript
Function.prototype.bind = function(context) {
  let self = this;
  return function() {
    return self.apply(context, arguments);
  };
};
```

- 借用其他对象的方法，示例：

```javascript
(function() {
  Array.prototype.push.call(arguments, 3); // [1,2,3]
})(1, 2);
```

```javascript
let obj = {
  name: "Jerry"
};
let func = function() {
  console.log(this.name); // "Jerry"
}.bind(obj);
func();
```

7. 闭包

作用：

- 封装变量：闭包可以帮助把一些不需要暴露在全局的变量封装成“私有变量”。

- 延长局部变量的生命周期，示例：

```javascript
let report = function(src) {
  let img = new Image();
  img.src = src;
};
report("http://xxx.com/getUserInfo");
```

上述 report 函数常用来数据上报，但在一些低版本浏览器中存在 bug，会丢失 30%左右的数据。因为 imge 是 report 函数中的局部变量，当 report 函数调用结束，img 变量即被销毁，而此时可能还没来得及发送 HTTP 请求。<br>
可以用闭包将 img 变量封闭起来，解决上面的问题。

```javascript
let report = (function() {
  let imgs = [];
  return function(src) {
    let img = new Image();
    imgs.push(img);
    img.src = src;
  };
})();
```

8. 高阶函数

- 高阶函数是至少满足下列条件之一的函数：函数可以作为参数被传递，函数可以作为返回值输出。JavaScript 中的函数显然满足高阶函数的条件。

- 函数作为参数传递：把函数作为参数传递，表示可以抽离出一部分容易变化的逻辑，将这部分放在函数参数中，分离代码中变与不变的部分。应用场景：回调函数、Array.prototype.sort。

- 回调函数，示例：<br>
  在 ajax 异步请求中，想在 ajax 请求返回后做一些事情，但又不知道请求返回的确切时间，最常见的方案就是把 callback 函数作为参数传入发起 ajax 请求的方法中，待请求完成后执行 callback 函数。

```javascript
let getUserInfo = function(userId, callback) {
  $.ajax("http://xxx.com/getUserInfo?" + userId, function(data) {
    if (typeof callback === "function") {
      callback(data);
    }
  });
};

getUserInfo(12313, function(data) {
  console.log(data.userName);
});
```

- 函数作为返回值输出

- 高阶函数的其他应用：<br>
  （1）函数柯里化（function currying）：一个 currying 的函数会接受一些参数，接受这些参数后，该函数不会立即求值，而是继续返回一个函数，刚才传入的参数在函数形成的闭包被保存起来。等到函数被真正需要求值的时候，之前传入的参数会被一次性用于求值。<br>
  （2）uncurrying<br>
  （3）函数节流<br>
  （4）分时函数<br>
  （5）惰性加载函数

9. 单例模式

- 单例模式：保证一个类只有一个实例，并提供一个访问它的全局访问点。

- 单例模式是一种常用的设计模式，有一些对象我们往往只需要一个，如线程池、全局缓存、浏览器中的 window 对象等等。

- 实现：用一个变量标志是否已经为某个类创建过对象，如果是，则在下一次获取该类的实例时，直接返回之前创建的对象。示例：

```javascript
let Singleton = function(name) {
  this.name = name;
  this.instance = null;
};
Singleton.prototype.getName = function() {
  console.log(this.name);
};

Singleton.getInstance = function(name) {
  if (!this.instance) {
    this.instance = new Singleton(name);
  }
  return this.instance;
};

let a = Singleton.getInstance("Tom"),
  b = Singleton.getInstance("Jerry");
console.log(a === b); // true
```

- 上述方式实现简单，但有一个问题，就是增加了这个类的“不透明性”，Singleton 的使用者必须知道这是一个单例类，和以往用 new 来获取对象不同，这里使用 Singleton.getInstance 来获取对象。下面将实现一个“透明”的单例类，用户从这个类创建对象，和其他任何普通类一样。示例：

```javascript
```

- 使用代理实现单例模式，示例：

```javascript
let CreateDiv = function(html) {
  this.html = html;
  this.init();
};

CreateDiv.prototype.init = function() {
  let div = document.createElement("div");
  div.innerHTML = this.html;
  document.body.appendChild(div);
};

// 代理类‘
let ProxySingletonCreateDiv = (function() {
  let instance;
  return function(html) {
    if (!instance) {
      instance = new CreateDiv(html);
    }

    return instance;
  };
})();

let a = new ProxySingletonCreateDiv("Tom"),
  b = new ProxySingletonCreateDiv("Jerry");
console.log(a === b);
```

### 《Node.js权威指南》
1. Node.js概述
- 在一个Web应用程序中，一个主要的瓶颈是服务器所支持的最大同时连接用户量。在Java、PHP等服务器端语言中，为每一个客户端连接创建一个新的线程，而在Node.js中，它并不为每个客户端连接创建新的线程，而是为每个客户端连接触发一个在Node.js内部进行处理的事件。因此，如果使用Node.js，可以同时处理多达几万个用户的客户端连接。

- 为实现高性能，Node.js采用了以下两种机制：非阻塞型I/O，事件环。

- Node.js适合开发的应用程序：当应用程序需要处理大量并发的输入/输出，而在向客户端发出响应之前，应用程序内部并不需要进行非常复杂的处理时。如：聊天服务器，综合服务类网站等。

2. Node.js的交互式运行环境——REPL(Read-Eval-Print-Loop)
- REPL：开发者可以在该环境中很方便地输入各种JavaScript表达式，并观察表达式的运行结果。

- REPL环境内部使用eval函数来评估该表达式的执行结果。

3. 全局作用域及全局函数

- 在Node.js中，在一个模块中定义的变量、函数或方法只能在该模块中可用，但可以通过exports对象将其传递到模块外部。

- 但是在Node.js中，仍然存在一个全局作用域，即可以定义一些不需要通过任何模块的加载即可使用的变量、函数或类。

- 在Node.js中，定义了一个global对象，代表Node.js的全局命名空间。任何全局变量、函数或对象都是该对象的一个属性值。

- 在Node.js中，可以使用require函数来加载模块。使用require.resolve函数来查询某个模块文件的带有完整绝对路径的文件名。

4. 事件处理机制与事件环机制
- 在Node.js的用于实现各种事件处理的event模块中，定义了一个EventEmitter类，所有可能触发事件的对象都是继承了EventEmitter子类的实例对象。

- 事件环机制：

5. 模块

- 在Node.js中，以模块为单位划分所有功能，每一个模块都是一个JavaScript脚本文件。它允许我们将第三方类库引入我们的应用程序中，也可以帮助我们将应用程序代码划分为不同的模块。Node.js包含以下几种模块文件：（1）后缀为.js的JavaScript脚本文件；（2）后缀为.json的JSON文本文件；（3）后缀为.node经过编译后的二进制模块文件。

- 可以通过exports对象将模块传递到模块外部，也可以将exports对象书写为"module.exports"，但是需要将模块定义为一个类时，只能使用"module.exports"的书写方法。

- 如果在require函数中只指定文件名，但不指定路径，那么Node.js将该文件视为node_modules目录下的一个文件。

6. 包
- 在Node.js中，可以通过包将一组具有依赖关系的模块进行统一管理，将某个独立的功能封装起来。
-一个包实际上是一个目录，通常包含以下内容：<br>
（1）在包的根目录中存放package.json文件（对包进行描述的JSON格式文件）；<br>
（2）在bin子目录存放二进制文件；<br>
（3）在lib子目录存放JavaScript文件；<br>
（4）doc子目录；<br>
（5）test子目录。

7. 使用Buffer类处理二进制数据
- 在处理Tcp流或文件流时，必须要处理二进制数据。因此在Node.js中，定义了一个Buffer类，该类用来创建一个专门存放二进制数据的缓存区。

8. 操作文件系统
- Node.js提供fs模块，实现文件及目录的读写操作。在fs模块中，所有对文件及目录的操作都可以使用同步与异步两种方法。

9. 实现基于TCP与UDP的数据通信
- Node.js提供net模块和dgram模块，分别用于实现基于TCP及UDP的数据通信。

- 在Node.js中，要创建一个TCP服务器，只需调用net模块中的createServer方法即可。

- 使用dgram模块中的createSocket方法创建一个用于实现UDP通信的socket端口对象。

10. 创建HTTP与HTTPS服务器及客户端
- Node.js提供http模块与https模块，用于创建HTTP服务器、HTTP客户端以及HTTPS服务器与HTTPS客户端。

11. 数据库访问

### 《工程数学线性代数 第六版》

1. 行列式

- 利用行列式求解二元线性方程组<br>

$$
\begin{cases}
a_{11}x_1+a_{12}x_2=b_1 \tag 1 \\
a_{21}x_1+a_{22}x_2=b_2 \\
\end{cases}
$$

方程组(1)的解为：

$$
\begin{cases}
x_1=\frac{b_1a_{22}-a_{12}b_2}{a_{11}a_{22}-a_{12}a_{21}} \\ & \text{if $a_{11}a_{22}-a_{12}a_{21} != 0$} \\
x_1=\frac{a_{11}b_2-b_1a_{21}}{a_{11}a_{22}-a_{12}a_{21}} \\
\end{cases}
$$

使用行列式进行表示：
$ D=\begin{vmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \\ \end{vmatrix},
D_1=\begin{vmatrix} b_1 & a_{12} \\ b_2 & a_{22} \\ \end{vmatrix},
D_2=\begin{vmatrix} a_{11} & b_1 \\ a_{21} & b_2 \\ \end{vmatrix}$

则：
$ x_1=\frac{D_1}{D}, x_2=\frac{D_2}{D} $

- 全排列：把 n 个不同的元素排成一列，叫做这 n 个元素的全排列。对于 n 个不同的元素，先规定各元素之间有个标准次序（例如规定从小到大为标准次序），当 1 对元素的先后次序与标准次序不同，就构成 1 个逆序。逆序数为奇数的排列叫做奇排列，逆序数为偶数的排列叫做偶排列。

- 对换：一个排列中任意两个元素对换，排列改变奇偶性。

- 行列式的一些性质：<br>
  （1）行列式和它的转置行列式相等；<br>
  （2）对换行列式的两行（列），行列式变号；<br>
  （3）行列式的某一行（列）中所有元素都乘以同一数 K，等于数 K 乘此行列式；<br>
  （4）行列式中有两行（列）元素成比例，则此行列式等于 0；<br>
  （5）若行列式中某一行（列）的元素都是两数之和，则该行列式等于下列两个行列式之和；<br>
  （6）把行列式的某一行（列）的各元素乘同一个数然后加到另一行（列）对应的元素上去，行列式不变。

- 代数余子式

````

```

```

```

```

```

```
````
