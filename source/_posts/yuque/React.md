---
title: React
urlname: nbv1mn
date: '2022-03-13 21:51:37 +0800'
tags: []
categories: []
---

change log
React 做了两件事：渲染 UI 和响应事件

性能提升
React 虚拟 dom 的数据结构时间复杂度是 O(n^3)，链表的数据结构时间复杂度是 O(n)，所以 React16.0 之后使用链表的数据结构。
因为 React16.0 之前的虚拟 dom 更新采用的是循环和递归，由于是线性的主线程会被一直占用，复杂的业务场景会出现卡顿。

Fiber
利用浏览器空闲时间执行，不会长时间占用主线程

- requestIdleCallback 浏览器 API，可暂停当前任务利用浏览器空闲时间执行优先级更高的任务。

将对比更新 dom 的操作碎片化
碎片化的任务，可以根据需要被暂停

生命周期
React 生命周期在 React16.0 版本加入了 Fiber 时发生了变化，您想听哪个？

- 初始化：constructor 设置 props 和 state
- 挂载：componentWillMount –> render –> componentDidMount
- 更新：
  - props 更新：componentWillReceiveProps –> shouldComponentUpdate –> componentWillUpdate –> render –> componentDidUpdate
  - state 更新：suouldComponentUpdate –> componentWillUpdate –> render –> componentDidUpdate
- 卸载：componentWillUnmount

面试复盘，录音，值得录音的面试

React diff 算法策略

- 针对树结构(tree diff)：对 UI 层的 DOM 节点跨层级的操作进行忽略。(数量少)

        type变化，比如div变成了p
        key变化

- 针对组件结构( component diff)：拥有相同类的两个组件生成相似的树形结构，拥有不同类的两个组件会生成不同的属性结构。
- 针对元素结构(element-diff)：对于同一层级的一组节点，使用具有唯一性的 id 区分(key 属性)

Fiber 算法

- 通过 state 计算出新的 Fiber 节点
- 对比节点的 tag 和 key 确定节点操作(修改，删除，新增，移动)
- effectTag 标记 Fiber 对象
- 收集所有标记的 Fiber 对象，形成 effectList
- commit 阶段一次性处理所有变化的节点

答题留有一定的空间，不要一次全部答完。
