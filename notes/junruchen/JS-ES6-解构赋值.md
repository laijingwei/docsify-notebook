解构赋值，就是按照一定的规则从数组或对象中取值，并赋值给相应的变量。

解构赋值的几点注意事项：
- 解构赋值等号右侧必须存在
- 等号右侧不是数组或者对象时，会先转换成对象，再继续操作。如果是`null`、`undefined`则抛出错误

主要内容
- [1、默认值](#es61)
- [2、对象的解构赋值](#es62)
- [3、数组的解构赋值](#es63)
- [4、函数的解构赋值](#es64)
- [5、圆括号](#es65)
- [6、Rest 不定元素...](#es66)

#### <a name="es61"></a>默认值
可以设置默认值，默认值只有在数组或对象的指定成员`严格等于undefined`时，才可以生效。

默认值可以是表达式，且表达式是惰性求值的，只有在用的时候，才会求值。

默认值也可以是已经声明的变量。

#### <a name="es62"></a>对象的解构赋值
对象的解构赋值是无序的，也可以为变量指定要匹配的模式，如：
```
let {foo: bar, baz} = {foo: 1, baz: 2}
console.log(bar) // 1
console.log(baz) // 2
```
- 上面例子中，`foo: bar`，等号左侧的foo为要匹配的模式，等号的右侧才是要声明的变量。
- `{foo: bar, baz}`其实是`{foo: bar, baz: baz}`的简写

#### <a name="es63"></a>数组的解构赋值
数组的解构赋值有有序的，若等号的右侧为不可遍历的解构，则会报错。

也可以使用`let [,,a] = [1, 2, 3]`的形式，只使用数组中某几个值声明变量。

#### <a name="es64"></a>函数的解构赋值
对于函数的参数，如果某参数使用了解构赋值且未指定默认值，则该参数为必填项目

#### <a name="es65"></a>圆括号
对于一个已经声明的变量，做`对象的解构赋值`操作时，应该用圆括号包起来，以防止错误解析，如：`{a, b} = {a:1, b:2}`

ES6规定，只能在非模式的部分，使用圆括弧。

注意：以下几种情况均不可使用圆括弧：
- 声明变量
- 函数参数
- 赋值语句中的模式部分

#### <a name="es66"></a>Rest 不定元素...
解构赋值中，如果使用了不定元素，则必须放在最后一个条目，否则会抛出语法异常：
```
// 常规用法
let [, ...otherbooks] = ['books', 'book1', 'book2', 'book3']
console.log(otherbooks) // ['book1', 'book2', 'book3']

let [, ...otherbooks, lastbook] = ['books', 'book1', 'book2', 'book3']
console.log(otherbooks, lastbook) // SyntaxError: Rest element must be last element


// 复合使用
let {name, list: [type, ...books]} = {name: 'ming', list: ['books', 'book1', 'book2']}
console.log(name, type, books) // ming books [book1, book2]
```
