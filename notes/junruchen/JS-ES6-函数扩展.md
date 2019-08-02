主要内容
- [1、函数默认参数值会影响arguments](#function1)
- [2、不定参数...](#function2)
- [3、展开运算符](#function3)
- [4、使用构造函数创建函数时，也支持不定参数与默认值](#function4)
- [5、函数的name属性](#function5)
- [6、new.target元属性](#function6)
- [7、箭头函数](#function7)
- [9、严格模式](#function8)
- [9、双冒号运算符::](#function9)

#### <a name="function1"></a>1、函数默认参数值会影响arguments
**注意，在使用函数默认参数时**：
- 不能使用同名参数
- length返回的长度会减去默认参数的个数以及不定参数，原因：length只会统计函数预期传入的参数个数。某个参数指定默认值以后，预期传入的参数个数就不包括这个参数了


在ES5中，严格模式下，arguments对象与命名参数保持分离，如：
```
function foo (a, b) {
    'use strict'
    console.log(a === arguments[0]) // true
    console.log(b === arguments[1]) // true
    a = 2
    b = 3
    console.log(a === arguments[0]) // false
    console.log(b === arguments[1]) // false
}
foo()
```
在ES6中，如果使用了参数默认值，那么arguments对象的行为与ES5严格模式下保持一致，如：
```
function foo (a, b = 3) {
    console.log(a === arguments[0]) // true
    console.log(b === arguments[1]) // false
    a = 2
    b = 3
    console.log(a === arguments[0]) // false
    console.log(b === arguments[1]) // false
}
foo(1)
```

#### <a name="function2"></a>2、不定参数...
将多个独立的参数明，整合成数组来访问
- length只会统计预期会传入的命名参数的个数，所有不定参数不参与统计
- 函数参数中，不定参数只能放在末尾，且只能存在一个
- 不能用在setter中，因为setter有且只能有一个参数
- 不会影响arguments

#### <a name="function3"></a>3、展开运算符
指定一个数组，打散后作为各自独立的参数传入函数
```
let arr = [3, 10, 2, 39, 9]
console.log(Math.max(...arr)) // 39
```

#### <a name="function4"></a>4、使用构造函数创建函数时，也支持不定参数与默认值，如：
```
let foo = new Function("a = 0", "...args", "return args")
console.log(foo(1, 2, 3, 4, 5)) // [2, 3, 4, 5]
```
注意：构造函数接收的是字符串形式的参数

#### <a name="function5"></a>5、函数的name属性
- name优先级，函数本身的名字优先级高于函数被赋值的变量
- 对于bind方法生成的函数，会在名称前加上`bound`前缀
- 对于构造函数生成的函数，会在名称前加上`anonymous`前缀

对象内部方法：
- 对于get与set，会在名称前加上`get|set`前缀
- 对于bind方法生成的函数，会在名称前加上`bound`前缀
- 对于构造函数生成的函数，会在名称前加上`anonymous`前缀
- 如果对象的方法是一个symbol值, name属性返回Symbol值的描述

```
const key1 = Symbol('description');
const key2 = Symbol();
let obj = {
  [key1]() {},
  [key2]() {},
};
obj[key1].name // "[description]"
obj[key2].name // ""
```

#### <a name="function6"></a>6、new.target元属性
元属性指非对象的属性

在使用new初始化类时，会调用类中的构造函数，这个过程自动执行了以下操作：
- 创建一个新对象
- 将构造函数中的作用域赋给新对象，即`this`指向新对象
- 执行构造函数中的代码
- 返回一个新对象

在函数内部有两个不同的内部方法：`[[Call]]`、`[[Construct]]`：
- 当使用new关键字调用函数时，执行`[[Construct]]`函数，负责创建一个实例，然后执行函数体，将this绑定到实例上；此时new.target被赋值为new操作符的目标，也就是新创建的实例。
- 非new调用的函bb数，执行`[[Call]]`函数，直接执行函数体；new.target值undefined。

注意：在函数外使用new.target是一个语法错误

#### <a name="function7"></a>7、箭头函数
- 无this、super、arguments和new.target绑定，这些值均是由外围最近一层非箭头函数决定
- 不能通过new关键字调用，无[[contract]]内部方法
- 没有原型
- 不能改变this的绑定
- 不支持arguments对象，只能通过命名参数和不定参数访问函数的参数
- 无论是不是严格模式，均不支持重复命名的参数。传统的函数中，只有严格模式才不允许定义重复参数

#### <a name="function8"></a>8、严格模式
ES5规定：函数内部可以使用严格模式

ES6规定：只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。

原因：函数内部的严格模式，同时作用于函数体和函数参数。在函数执行的时候，先执行函数参数，再执行函数体。但是只有从函数体之中，才能知道参数是否应该以严格模式执行。

#### <a name="function9"></a>9、双冒号运算符::
用来取代bind调用。

双冒号的左边是一个对象，右边是一个函数。该运算符会自动将左边的对象，作为上下文环境，绑定到右边的函数上面。

```
foo::bar(a)
等同于
bar.bind(foo, a)

foo::bar
等同于
bar.bind(foo)
```