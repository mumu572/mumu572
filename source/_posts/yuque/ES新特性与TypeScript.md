---
title: ES新特性与TypeScript
urlname: ocmg9x
date: '2021-05-26 15:47:31 +0800'
tags:
  - ES6
categories:
  - JavaScript
---

我们常说 ECMAScript 是一种脚本语言，通常我们把 ECMAScript 看做是一种标准化规范，而实际上是 JavaScript 是 ECMAScript 的扩展语言。

在浏览器环境中，JavaScript 等于 ECMAScript 加上 WEB API(DOM+BOM)

在 NodeJs 环境中，JavaScript 等于 ECMAScript 加上 Node APIS(fs、net、etc.)

所以，JavaScript 语言本身指的就是 ECMAScript。

由于 ES5.1 以后的版本相较于之前有了很大的改动，有很多人就习惯简称它们为 ES6，其实他的准确简称应该是 ES2015。

## ES2015 let 与块级作用域

var 会被变量提升，let 不会有这个问题

## ES2015 const

const 声明的常量不能再次修改引用的内存地址。

## ES2015 数组的解构

const [a.b] = [100, 200]
可以根据位置提取对应的值

## ES2015 对象的解构

const {a} = {a:200}
和数组不同的是，它需要指定解构的属性名

## ES2015 模板字符串

和传统的字符串相比，支持多行字符串，还可以使用插值表达式拼接内容，而不用像传统字符串用+号拼接，更便捷。

## ES2015 带标签的模板字符串

const str = console.log'hello wolrd'
模板字符串前面可以带上一个函数，这个函数中可以接收到所有表达式出现的值。

## ES2015 字符串的扩展方法

startWith
endWith
includes

## ES 2015 参数默认值

function fn(a = 100){}
可以在形参后面加上=值
一定要将需要添加默认值的形参放在最后，不然可能导致参数默认值无法正常工作。比如:
function fn(a=100,b){}
fn(100) //我想要形参 a 有一个默认值，但是我可能只会传这一个参数，a 的参数默认值就不能正常工作。
因为参数是依次传递的，可选的参数应该放在后面，保证必传的参数能够优先传递。

## ES2015 剩余参数

arguments
...args

## ES2015 展开数组

console.log(...[100,200,300])

## ES2015 箭头函数与 this

在箭头函数中没有 this，它的 this 指向它的上级作用域。

## ES2015 对象字面量的增强

对象中可以省略属性名对应的值，前提是属性名和字面量名称相同。

## ES2015 Object.assign

var obj3=Object.assign(obj1, obj2)
用 obj2 覆盖 obj1 对象，返回的 obj3 它其实就是 obj1

## ES2015 Object.is

==只比较值，不比较类型，会自动类型转换
===比较值和类型，严格模式
NaN ===NaN //false
Object.is(NaN,NaN)//true

## ES2015 Proxy

可以对对象的属性改动进行检测和拦截

## ES2015 Proxy 对比 Object.defineProperty

Proxy 功能更强大一些。
proxy 能够检测 defineProperty 检测不到的行为，比如属性删除，方法调用
可以对数组检测
Proxy 是一种非侵入式的方式进行代理，不用对原来的对象做任何改动，而 Object.definePropery 则需要我们对原对象做一些特有的改动。

## ES2015 Reflect

Reflect.get
Reflect.set
提供了一套对对象操作的 api
以前的操作方式可能会被废弃掉

## ES2015 Promise

异步编程解决方案

## ES2015 class

## es2015 静态方法

## es2015 类的继承

super

## ES2015 Set

不重复的数组 常用来去重

## ES2015 Map

let obj ={a:100}
let o = new Map()
o.set(obj, 666) //它的键就是 obj 对象本身
严格的键值对集合，它的键可以是任意类型。

## ES2015 Symbol

Symbol 表示独一无二的值，他可以作为对象的键( key)。

#### Symbol.for

内部维护了一个全局的注册表，提供了字符串和 Symbol 的映射关系。

```javascript
// 因此Symbol.for("aa") = Symbol. for("aa") // true
// 如果传入的不是字符串，会自动转换为字符串。
Symbol.for(true) === Symbol.for(" true"); // true
```

#### Symbol 用途

1. 我们在使用第三方模块时，想要对其扩展，由于我们不知道内部具体定义的哪些属性，在这种情况下，去为其扩展属性，就会很大可能发生冲突的问题。那么使用`Symbol`作为属性就不会出现这种问题。
1. 可以为对象添加私有属性

```javascript
const name = Symbol()
class Person {
  [name]: "xsl",
    say(){
    // 只能通过这种方式访问
    console.log(this.[name])
  }
}
// 而当我们在外部使用时，由于不知道内部的唯一键是什么，因此只能通过实例间接访问，而无法在外部直接访问。
const obj = new Person()
console. log(obj.say)
```

3.  `Symbol`提供了很多内置常量，用于作为内部方法的标识。这些标识符可以让自定义对象实现 JS 当中内置的接口。比如：

```javascript
// Symbol.iterator
// Symbol.hasInstance
// Symbol.toStringTag
const obj = {
  [Symbol.toStringTag]: "XObject",
};
console.log(obj.toString()); // [ object XObject]
```

对象的`Symbol`属性无法通过`for in`和`Object.keys`获取，`JSON.stringify`时`Symbol`的属性也会被忽略掉。
**可以使用**`**Object.getOwnPropertySymbols**`**获取对象的所有**`**Symbol**`**类型的属性。**

## ES2015 for of

使用 for of 可以遍历所有数据类型
默认可以对数组遍历
需要实现统一的 Iterable 接口，数组默认内部已经实现了。

## ES2015 Iterable

## ES2016 概述

## ES2017 概述

允许在参数和数组字面量后边加上小逗号
