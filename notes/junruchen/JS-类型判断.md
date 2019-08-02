- 基本数据类型 number string boolean null undefined symbol
- 引用类型 object function array regExp等

### typeof
* 未定义、未初始化：返回`"undefined"`
* 布尔值：返回`"boolean"`
* 字符串：返回`"string"`
* 数值(包括NAN)：返回`"number"`
* 对象、null：返回`"object"`， null 表示空对象指针
* 函数：返回`"function"`

**注意**： `typeof`可以判断基本类型，无法判断对象的类型或者null

### instanceof
语法：`variable instanceof constructor`

如果变量是引用类型，可以使用instanceof判断，检测基本类型时，会返回false。

原理：判断变量的原型链上是否有构造函数的prototype属性

如：
```
// 判断person是否是object类型对象
person instanceof Object
```

**注意：空对象{}的判断问题**
```
let obj1 = {}
console.log(obj1 instanceof Object) // true

let obj2 = Object.create(null)
console.log(obj2 instanceof Object) // false

let obj3 = Object.create({})
console.log(obj3 instanceof Object) // true
```

#### Object.prototype.toString
所有的数据类型都可以使用此方法进行检测，且非常精准。
如：
```
let obj = {}
Object.prototype.toString.call(obj) === '[object Object]'
```

#### 总结
* **typeof** 适合基本类型和function类型的检测，无法判断null与object
* **instanceof** 适合自定义对象，也可以用来检测原生对象，在不同的iframe 和 window间检测时失效，还需要注意`Object.create(null)`对象的问题
* **{}.toString** 适合内置对象和基元类型，遇到null和undefined失效（IE678返回[object Obejct]）