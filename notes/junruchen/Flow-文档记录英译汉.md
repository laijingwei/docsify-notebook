> 持续更新中

## Flow介绍

Flow是一个作用于JavaScript语言的静态类型检查程序。

示例：

    // @flow
    function square(n: number): number {
        return n * n;
    }
    square("2"); // Error!
Flow可以很好的理解JavaScript语言。上述例子中我们只需要使用少量的类型描述，Flow就可以准确检测类型错误。很多时候，Flow可以理解我们的代码可以不需要任何类型描述。如下代码所示：

    // @flow
    function square(n) {
        return n * n;
    }
    square("2"); // Error!

## Primitive Type (原始类型)
* Booleans
* Strings
* Numbers
* null
* undefined (在Flow中类型使用void代替)
* Symbols (Flow不支持)

#### 原始类型在flow中有两种存在形式：
1、以值的形式出现，此时类型需要小写，如：

    // @flow
    function method (x: number, y: string){
        // ...
    }
    method(3.2, 'hello')

2、以包装对象的形式出现(JS中基础包装对象有三种，分别是Number，String和Boolean)，此时类型需要首字母大写，类似构造函数，如：

    // @flow
    function method (x: Number, y: String){
        // ...
    }
    method(new Number(42), new String('hello'))

#### 值得注意的是：
* JS可以对类型进行隐式转换，在使用Flow时，需要显示转换。
* **boolean和Boolean**是两种不同的类型。boolean类型的值应该是`true`、`false`或者是一个类似`a === b`的表达式；Boolean类型的值应该是`new Boolean(x)`，使用new和构造函数创建出来的值。
* **number和Number**是两种不同的类型。number类型的值应该是`3`、`3.14`或者是一个类似`parseFloat(x)`的表达式；Number类型的值应该是`new Number(x)`，使用new和构造函数创建出来的值。
* JS允许字符串拼接其他类型的值，Flow只支持字符串拼接字符串或者数字
* **string和String**是两种不同的类型。string类型的值应该是`"foo"`、`"foo" + 42`或者是一个类似`parseFloat(x)`的表达式；String类型的值应该是`new String(x)`，使用new和构造函数创建出来的值。
* **void**类型表示**undefined**，undefined与null是两个不同的类型。

#### 不确定类型
在类型是可选的时，可以为类型添加一个`？`标记，如：`?string`。
#### 可选的对象属性
对象类型支持设置可选属性，如`{propertyNmae?: string}`，这些可选属性除了自身设置的类型，也支持void类型以及完全忽略该字段，但是不支持null

    // @flow
    function acceptsObject(value: {foo? string}) {
        // ...
    }
    acceptsObject({foo: 'bar'}) // Works!
    acceptsObject({foo: undefined}) // Works!
    acceptsObject({foo: null}) // Error!
    acceptsObject({}) // Works!

#### 可选的函数属性
在属性名后增加`？`标记，表示该属性为可选项。可选属性除了自身设置的类型，也支持void类型以及完全忽略该字段，但是不支持null

    // @flow
    function acceptsString(value?: string) {
        // ...
    }
    acceptsObject('bar') // Works!
    acceptsObject(undefined) // Works!
    acceptsObject(null) // Error!
    acceptsObject() // Works!

#### 有默认值的函数属性
在属性的类型后增加默认值。这些属性除了自身设置的类型，也支持void类型以及完全忽略该字段，但是不支持null

    // @flow
    function acceptsString(value: string = 'foo') {
        // ...
    }
    acceptsObject('bar') // Works!
    acceptsObject(undefined) // Works!
    acceptsObject(null) // Error!
    acceptsObject() // Works!

## Literal Type (值类型)

Flow也支持使用具体的值作为类型。
如下示例，使用数字2作为类型:

    // @flow
    function acceptsTwo(value: 2) {
        // ...
    }
    acceptsTwo(2) // Works!
    acceptsTwo(3) // Error!
    acceptsTwo('2') // Error!

这种类型的用处很广泛，最常见的用法如下：

    // @flow
    function getColor(name: 'success' | 'warning' | 'danger') {
        switch (name) {
            case 'success': return 'green'
            case 'warning': return 'yellow'
            case 'danger': return 'red'
        }
    }
    acceptsTwo('success') // Works!
    acceptsTwo('danger') // Works!
    acceptsTwo('error') // Error!

## Mixed Types(混合类型)

### 常见的三种类型
#### 一、单一类型
如下示例中函数参数只能是数字

    // @flow
    function square (n: number) {
        return n * n
    }

#### 二、一组类型
如下示例中参数可以是数字或者字符串

    // @flow
    function stringifyBasicValue (value: string | number) {
        return '' + value
    }

#### 三、依赖其他类型
如下示例中将会返回一个类型，该类型与函数接收到的参数类型一致

    // @flow
    function identity<T>(value: T): T {
        return value;
    }

### 任意类型
使用`mixed`，表示可以是任意类型。

    // @flow
    function getTypeOf(value: mixed): string {
        return value;
    }

注意：
当使用mixed类型时，必须先计算传入参数的实际类型，然后再进行其他操作，否则将报错。

示例一：不进行类型判断的情况会提示错误

    // @flow
    function stringify(value: mixed) {
        return value + ''; // Error!
    }
    stringify('foo')

示例二：使用`typeof value === 'string'`进行类型校验时，flow可以知道在if中只接受string类型

    // @flow
    function stringify(value: mixed) {
        if(typeof value === 'string') {
            return value + ''
        } else {
            return ''
        }
    }
    stringify('foo')

## Any Types(任何类型)

使用any类型是不安全的，应该尽可能的避免

比如下面的代码，不会提示任何错误：

    // @flow
    function add(n: any, m: any):number {
        return n + m
    }
    add(1, 2) // Works
    add('1', '2') // Works
    add({}, []) // Works

flow也不能捕捉到将会运行错误的代码

    // @flow
    function getNestedProperty(obj: any) {
        return obj.foo.bar.baz
    }
    getNestedProperty({})


#### 避免内存泄露问题
当对一个类型为any的值进行操作时，flow会认为操作的执行结果类型也是any，再对结果进行操作，操作的新结果也会被认为是any类型。可以持续这个过程any类型出现在代码的所有位置

如下示例，函数fn返回的结果类型为any，函数内部以及使用函数返回值的变量类型都为any

    // @flow
    function fn(obj: any) {
        let foo = obj.foo // foo类型为any
        let bar = foo * 2 // bar类型为any
        return bar
    }
    let bar = fn({foo: 2}) // bar类型为any
    let baz = 'baz:' + fn({foo: 2}) // baz类型为any

**可以使用快速定义其他类型的方式来解决上述问题**
如：

    // @flow
    function fn(obj: any) {
        let foo: number = obj.foo
        let bar = foo * 2 // bar类型为number
        return bar
    }
    let bar = fn({foo: 2}) // bar类型为number
    let baz = 'baz:' + fn({foo: 2}) // baz类型为string

## Maybe Types(可能类型)

使用`？`标志，表示该参数的类型可能是`设置的类型`，也可能是`null`或者`undefined`

如：

    // @flow
    function acceptsMaybeNumber(n: ?number) {
        return n
    }
    acceptsMaybeNumber(2) // Works
    acceptsMaybeNumber(null) // Works
    acceptsMaybeNumber(undefined) // Works
    acceptsMaybeNumber() // Works
    acceptsMaybeNumber('234') // Error

使用`value != null`可以同时排除`undefined`和`null`的值，也可以使用其他类似`typeof`的方式来校验排除

## Variable Types(变量类型)

使用`let`或者`var`声明的变量可以被重新赋值，使用`const`声明的是常量，不可重新赋值

#### const
flow可以从值中提取类型，也可以给常量设置一个类型

    // @flow
    const foo: number = 2
    const foo = 2

#### var let
与`const`类似，flow可以从值中提取类型，或者为变量设置一个类型

    // @flow
    let foo: number = 2
    let foo = 2

当变量被设置类型时，修改变量必须可兼容的类型

    // @flow
    let foo: number = 2
    foo = 3 // Works!
    foo = '4' // Error!

下面这些情况下，flow可以知道变量修改后的类型。

    // @flow
    let foo = 2
    let isNumber: number = foo // Works!

    foo = '4'
    let isString: string = foo

if语句、函数和其他判断代码运行时jjiang hu将会阻止flow计算类型

    // @flow
    let foo = 42;
    function mutate() {
        foo = true;
        foo = "hello";
    }
    mutate();
    // $ExpectError
    let isString: string = foo; // Error!

## function Types(函数类型)

函数可以设置两个地方的类型，一是接收的参数类型，二是返回的类型。

    // @flow
    function concat(a: string, b: string): string {
        return a + b;
    }
    concat("foo", "bar"); // Works!
    // $ExpectError
    concat(true, false);  // Error!

#### 函数声明
有类型和无类型

    // @flow
    function method(str, bool, ...nums) {
        // ...
    }
    function method(str: string, bool: boolean, ...nums: Array<number>): void {
        // ...
    }

#### 箭头函数

    // @flow
    let method = (str, bool, ...nums) => {
        // ...
    }
    let method = (str: string, bool: boolean, ...nums: Array<number>): void => {
        // ...
    }

#### 函数类型
1、常见写法

    (str: string, bool?: boolean, ...nums: Array<number>) => void

2、可以省略参数名称

    (string, boolean | void,  Array<number>) => void

3、也可以像回调函数一样使用这些函数类型

    function method(callback: (errpr: Error | null, value: string | null) => void {
        // ...
    }

#### 函数参数类型设置

    function method(param1: string, param2: number) {
        // ...
    }

如果属性为可选项，可以使用在属性名后加`?`标记的形式进行标注。

    function method(param?: string) {
        // ...
    }
此时，函数参数可以是空，undedined，以及符合类型的值，但是不支持null

#### 函数接收的参数组 arguments
可以为函数接收的参数组指定类型，类型必须是数组，也可以为数组指定类型，如果示例，要求属性类型为数字

    function method(...args: Array<number>) {
        // ...
    }

#### 函数返回值的类型
函数返回值类型可以确保函数的每个分支都返回相同的类型。

    function method(...args: Array<number>): number {
        // ...
    }

#### this
在flow中，不需要为this添加注释，flow会自动检查

    function method() {
        return this;
    }
    var num: number = method.call(42);
    // $ExpectError
    var str: string = method.call(42);

#### 函数内部判断
在函数内部使用if条件判断语句时，直接使用if判断，flow会提示错误，需要使用flow提供%checks注释，如：

    function truthy(a, b): boolean %checks {
        return !!a && !!b;
    }
    function concat(a: ?string, b: ?string): string {
        if (truthy(a, b)) {
            return a + b;
        }
        return '';
    }


## Object Types(对象类型)
#### 基础语法
使用花括号

    // @flow
    let obj1: {foo: boolean} = {foo: true}
    let obj2: {
        foo: number,
        bar: boolean
    } = {
        foo: 1,
        bar: true
    }

#### 可选的对象属性
在js中访问对象不存在的属性，会提示错误，在flow中，同样会报错。

为对象设置可选属性，如下示例，可选属性的值不可为null

    // @flow

    function acceptsObject(value: { foo?: string }) {
        // ...
    }
    acceptsObject({ foo: "bar" });     // Works!
    acceptsObject({ foo: undefined }); // Works!
    acceptsObject({ foo: null });      // Error!
    acceptsObject({});

#### 创建有属性的对象
当创建一个带有属性的对象时，flow不允许添加新的属性，如下示例

    // @flow
    let obj = {
        foo: 1
    };
    // $ExpectError
    obj.bar = true;    // Error!
    // $ExpectError
    obj.baz = 'three'; // Error!
#### 没有任何属性的对象
当创建一个没有任何属性的对象时，flow允许添加新的属性，且推断出新添加的属性类型

    // @flow
    let obj = {};
    obj.foo = 42;
    let num: number = obj.foo;

注意：属性重新赋值时，flow也会重新计算类型。另外在这一类对象中查找未声明的属性是不安全的。

#### 确定的对象类型
当对象的类型是确定时，不允许添加其他属性。

    // @flow
    // Error!
    let foo: {| foo: string |} = { foo: "Hello", bar: "World!" };

#### Map Objects
语法：

    // @flow
    let o : {[string]: number} = {}
    o['foo'] = 1
    o['bar'] = 2

也可以为属性添加描述，如：

    // @flow
    let o : {[user_name: string]: number} = {}
    o['foo'] = 1
    o['bar'] = 2