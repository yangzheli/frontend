## 读书总结

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

9. 原始值与引用值

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

10. 变量作用域

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

11. 垃圾回收与内存管理

- JavaScript 是使用垃圾回收的语言，垃圾收集器会定时、周期性地找出不再继续使用的变量，然后释放其占用的内存。标识无用变量的策略通常有两种：<br>
  （1）标记清除（最常用）：垃圾收集器会给内存中所有变量都加上标识，然后去掉环境中的变量和被环境中变量引用的变量的标识，之后仍然被加上标识的变量就会被垃圾收集器回收所占用的内存。<br>
  （2）引用计数：跟踪每个值被引用的次数，当这个值的引用次数变为 0，其占用的内存空间就会被回收。

- 将内存占用量保持在一个较小的值可以让页面性能更好，优化内存占用的最佳手段就是保证在执行代码时只保存必要的数据。如果数据不再必要，就解除引用，比如把它设置为 null；

12. 原始值包装类型

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

13. 内置对象

- 除了 Object、Array、Function 和原始值包装对象，ECMAScript 还定义了另外 2 种内置对象：Global 和 Math；
- Global：
- Math：

14. 引用类型

- Object
- Array：数组中每个槽位可以存储任意类型的数据，即可以创建一个数组，它的第一个元素是字符串，第二个元素是数值，第三个元素是对象。ECMAScript 数组是动态大小的，会随着数据添加而自动增长；
- 定型数组
- Map（ES6 新增）：键/值对，与 Object 只能使用数值、字符串和符号作为键不同，Map 可以使用任何 JavaScript 数据类型作为键；
- WeakMap（ES6 新增）：弱映射，WeakMap 中的 “weak” 描述的是 JavaScript 垃圾回收程序对待弱映射中键的方式。弱映射中的键只能是 Object 或继承自 Object 的类型，使用非对象设置键会抛出 TypeError，值类型没有限制；WeakMap 中的键不属于正式的引用，不会阻止垃圾回收；WeakMap 无法对键/值对进行迭代。
- Set（ES6 新增）：一种新的集合类型，Set 可以包含任何 JavaScript 数据类型作为值；
- WeakSet（ES6 新增）：弱集合，WeakSet 中的 “weak” 描述的是 JavaScript 垃圾回收程序对待弱集合中值的方式。弱集合中的值只能是 Object 或继承自 Object 的类型，使用非对象设置键会抛出 TypeError。WeakSet 中的值不属于正式的引用，不会阻止垃圾回收。WeakSet 无法对值进行迭代。
- Function

15. 迭代器与扩展操作符
