继承的目的：将父级【Super】的属性变成自己的属性，且实例之间不会互相影响；共用父级原型【Super.prototype】中的方法。

- [原型链与构造函数结合方法继承](#prototype)
- [原型式继承](#create)

### <a name="prototype"></a>原型链与构造函数结合方法继承
1）原型链的方式直接实现继承
```
function Super () {
  this.type = 'super'
  this.colors = ['red', 'blue', 'black']
}
function Child (name) {
  this.type = 'child'
  this.name = name
}
Child.prototype = new Super()
Child.prototype.constructor = Child
var child1 = new Child('cat')
var child2 = new Child('dog')

// 问题一：引用类型值的原型属性会被所有实例共享，所以当其中一个修改时，其他实例也会接收到变化
child2.colors.push('pink')
console.log(child1.colors) // [ 'red', 'blue', 'black', 'pink' ]
console.log(child2.colors) // [ 'red', 'blue', 'black', 'pink' ]

// 问题二：没法向父级构造函数【Super】传递参数
```
2）构造函数的方式实现继承

使用call或者apply的方式获取到父级元素的属性和方法。
```
function Super () {
  this.type = 'super'
  this.colors = ['red', 'blue', 'black']
}
function Child (name) {
  Super.call(this)
  this.type = 'child'
  this.name = name
}
var child = new Child('cat')

// 优势一：call或者apply的方式，可以传递参数，可以解决原型链中无法传递参数的问题
// 问题一：只能在父级构造函数中定义方法，所以函数无法复用
// 问题二：不能继承原型中的方法
```

**3）使用原型链与构造函数相结合的方式实现继承**
```
function Super () {
  this.type = 'super'
  this.colors = ['red', 'blue', 'black']
}
function Child (name) {
  Super.call(this)
  this.type = 'child'
  this.name = name
}
Child.prototype = new Super()
Child.prototype.constructor = Child
var child1 = new Child('cat')
var child2 = new Child('dog')

child2.colors.push('pink')
console.log(child1.colors) // [ 'red', 'blue', 'black' ]
console.log(child2.colors) // [ 'red', 'blue', 'black', 'pink' ]
```

### <a name="create"></a>原型式继承Object.create()

**ES6中，Class使用extends关键字继承的原理**

通过Object.create()可以继承到Super.prototype的方法，在使用call或者apply获取到Super的属性
```
function Super () {
  this.type = 'super'
  this.colors = ['red', 'blue', 'black']
}
function Child (name) {
  Super.call(this)
  this.type = 'child'
  this.name = 'name'
}
Child.prototype = Object.create(Super.prototype)
Child.prototype.constructor = Child
var child = new Child('cat')
```

**注意：**
其中
```Child.prototype = Object.create(Super.prototype)```
可以使用以下方法代替：
```
Object.setPrototypeOf(Child.prototype, Super.prototype)
Child.prototype.__proto__ = Super.prototype
```

**Object.create()**
接收两个参数：新对象原型的对象；[可选]新对象定义额外属性的对象

当只传递一个参数时，Object.create()相当于做了以下事情：
```
function object (o) {
  function F () {}
  F.prototype = o
  return new F()
}
```
第二个参数为【新对象定义额外属性的对象】，对象中的每一个属性都是通过自己的描述符定义的，与Object.defineProperties()的第二个参数格式相同。且以这种方式指定的属性会覆盖原型对象上的原始属性。

如：
```
var person = {
  name: 'test',
  age: 20
}

var newPerson = Object.create(person, {
  name: {
    value: 'newName'
  }
})
```