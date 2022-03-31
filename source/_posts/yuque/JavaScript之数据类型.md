---
title: JavaScript之数据类型
urlname: sk8ag5
date: '2022-03-10 09:44:19 +0800'
tags: []
categories: []
---

## JS 中的数据类型被分为两大类：

#### 原始值类型（值类型/基本数据类型）

1. number 数字
1. string 字符串
1. boolean 布尔
1. null 空对象指针
1. undefined 未定义
1. symbol 唯一值
1. bigint 大数

#### 对象类型（引用数据类型）

1. 标准普通对象 `Object`
1. 标准特殊对象 `Array`、`RegExp`、`Date`、`Math`、`Error`......
1. 非标准特殊对象 `Number`、`String`、`Boolean`
1. 可调用/执行对象（函数） `Function`

## 数据类型检测的方式（4 种）

1. `typeof [value]` 返回值是字符串，字符串中包含所属的类型
   1. typeof 检测对象类型，除函数被识别'function'，其余都是'object'（不能细分对象）
   1. 基于 typeof 检测一个未被声明的变量，不会报错，结果是'undefined'
   1. `typeof null -> 'object'` typeof 检测 null 结果是'object'的原因是：如果是以'000'开始的二进制，则被识别为对象(null 存储的二进制都是 0，符合以'000'开始)；然后再去看对象是否实现了[[call]]，实现了则为函数(返回'function')，没实现就是对象(返回'object')
2. `Object.prototype.toString.call([value])`
3. `[value] instanceof [constructor]`
4. `[value].constructor`

其他检测固定类型的方法：`Array.isArray([value])`、`isNaN([value])` ......
检测是否为对象：`val !== null && /^(object|function)$/i.test(typeof val)`
0.1 + 0.2 != 0.3 计算机是二进制形式存储数据的，十进制浮点数在转换为二进制时，由于计算机存储位数限制，有可能出现精度丢失。
运算保证精度，实现思路：把小数变成整数(乘以系数)运算，运算后的结果再除以系数。

```javascript
const coefficent = function coefficent(num) {
  num = String(num);
  const [, char = ""] = num.split("."),
    len = char.length;
  return Math.pow(10, len);
};
```

```javascript
const plus = function plus(n, m) {
  n = Number(n);
  m = Number(m);
  let coeffic = Math.max(coefficient(n), coefficent(m));
  return (n * coeffic + m * coeffic) / coeffic;
};
```

## 数据类型转换

一般将其他数据类型转换为`Number`、`String`、`Boolean`

#### 把其他类型值转换为`Number`

1. `Number([value])`
1. `parseInt([val],[radix])`、`parseFloat([val])`

#### 把其他类型值转换为`String`

1. `[value].toString()`
1. `String([value])`

#### 把其他类型值转换为`Boolean`

转换规则：除了“0/NaN/空字符串/null/undefined”五个值是 false，其余的都是 true
出现情况：

1. `Boolean([val])`或者`!/!!`
1. `条件判断`
