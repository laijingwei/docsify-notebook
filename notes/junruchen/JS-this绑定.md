
- [改变this绑定的主要方式](#this)
- [call、apply、bind的用法与区别](#differ)
- [bind绑定原理](#bind)


#### <a name="this"></a>改变this绑定的主要方式
1）最常用的call()、apply()、bind()方法，如：
```
function foo () {
    this.count++
}
const obj = {
    count: 10
}
foo.call(obj)

console.log(obj.count) // 11
```

2）new绑定
```
let count = 10
function Foo (count) {
    this.count = count
}

let obj = new Foo(20)

console.log(count, obj.count) // 10 20
```

在使用new初始化类时，会调用类中的构造函数，这个过程自动执行了以下操作：
- 创建一个新对象
- 将构造函数中的作用域赋给新对象，即`this`指向新对象
- 执行构造函数中的代码
- 返回一个新对象

在函数内部有两个不同的内部方法：`[[Call]]`、`[[Construct]]`：
- 当使用new关键字调用函数时，执行`[[Construct]]`函数，负责创建一个实例，然后执行函数体，将this绑定到实例上；此时new.target被赋值为new操作符的目标，也就是新创建的实例。
- 非new调用的函bb数，执行`[[Call]]`函数，直接执行函数体；new.target值undefined。

注意：不是所有的函数都存在`[[Construct]]`方法，如箭头函数就没有，因为箭头函数也不能通过new调用。

3）在函数引用存在上下文时，会将函数调用中的this绑定到上下文对象，且只会绑定到引用链中的最后一层。
```
let count = 10
function foo () {
    this.count++
}

let obj = {
    count: 20,
    foo: foo v
}

obj.foo()
console.log(count, obj.count) // 10 21
```

4）箭头函数以及ES6中类的箭头函数属性，在使用箭头函数时，上下文取决于最近的非箭头函数的作用域

5）双冒号运算符，ES6引入来代替bind绑定

6）ES6中类的箭头函数属性也可以实现更改this的绑定

#### <a name="differ"></a>call、apply、bind的用法与区别
bind:
- bind绑定后，第一次之后的其他绑定均无法生效

共同点：
- 都是实现this绑定的切换
- 当传入的第一个参数为基本类型时，会先转换成为引用类型，当参数不存在或着为null时，均会报错；

区别：
- call与apply唯一的区别是：接收作为函数执行参数的格式不同，apply必须是数组的格式，call则是按顺序接收多个参数
- call与apply会立即调用；而bind()方法返回一个新的函数，需要触发才可执行，在运行时，原本bind()传递的除第一个之外的参数 + 运行时传入的参数，按顺序，作为被执行函数的参数

#### <a name="bind"></a>bind绑定原理
```
if (!Function.prototype.bind) {
  Function.prototype.bind = function (oThis) {
    if (typeof this !== 'function') {
      // closest thing possible to the ECMAScript 5
      // internal IsCallable function
      throw new TypeError('Function.prototype.bind - what is trying to be bound is not callable')
    }

    var aArgs = Array.prototype.slice.call(arguments, 1),
      fToBind = this,
      fNOP = function () {
      },
      fBound = function () {
        // this instanceof fNOP === true时,说明返回的fBound被当做new的构造函数调用
        return fToBind.apply(this instanceof fNOP
            ? this
            : oThis,
          // 获取调用时(fBound)的传参.bind 返回的函数入参往往是这么传递的
          aArgs.concat(Array.prototype.slice.call(arguments)))
      }

    // 维护原型关系
    if (this.prototype) {
      // Function.prototype doesn't have a prototype property
      fNOP.prototype = this.prototype
    }
    // 下行的代码使fBound.prototype是fNOP的实例,因此
    // 返回的fBound若作为new的构造函数,new生成的新对象作为this传入fBound,新对象的__proto__就是fNOP的实例
    fBound.prototype = new fNOP()

    return fBound
  }
}
```