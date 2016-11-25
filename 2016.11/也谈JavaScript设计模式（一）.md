# 也谈JavaScript设计模式（一）



注：*一直有关注前端行业动态，对目前主流框架也有些了解。从老牌的Backbone到新锐React & Vue & Weex。最近在做新的技术架构选型，面对琳琅满目的框架，到底如何选择，也是一门技术活。面对如此多的入门教程，在这里，我想谈一谈前端JavaScript的设计模式。希望能够通过这个系列的文章，帮助读者从另一个角度看待流行框架。*

文中提到的设计模式，均是只软件工程领域。

## What

设计模式是一种可复用的解决方案，可用于解决软件设计中遇到的常见问题。

> 在[软件工程](https://zh.wikipedia.org/wiki/%E8%BB%9F%E9%AB%94%E5%B7%A5%E7%A8%8B)中，**设计模式**（design pattern）是对[软件设计](https://zh.wikipedia.org/wiki/%E8%BB%9F%E4%BB%B6%E8%A8%AD%E8%A8%88)中普遍存在（反复出现）的各种问题，所提出的解决方案。这个术语是由[埃里希·伽玛](https://zh.wikipedia.org/wiki/%E5%9F%83%E9%87%8C%E5%B8%8C%C2%B7%E4%BC%BD%E7%91%AA)（Erich Gamma）等人在1990年代从[建筑设计](https://zh.wikipedia.org/wiki/%E5%BB%BA%E7%AD%91%E8%AE%BE%E8%AE%A1)领域引入到[计算机科学](https://zh.wikipedia.org/wiki/%E8%A8%88%E7%AE%97%E6%A9%9F%E7%A7%91%E5%AD%B8)的。
>
> 设计模式并不直接用来完成[代码](https://zh.wikipedia.org/wiki/%E7%A8%8B%E5%BC%8F%E7%A2%BC)的编写，而是描述在各种不同情况下，要怎么解决问题的一种方案。[面向对象](https://zh.wikipedia.org/wiki/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1)设计模式通常以[类别](https://zh.wikipedia.org/wiki/%E9%A1%9E%E5%88%A5)或[对象](https://zh.wikipedia.org/wiki/%E7%89%A9%E4%BB%B6_(%E9%9B%BB%E8%85%A6%E7%A7%91%E5%AD%B8))来描述其中的关系和相互作用，但不涉及用来完成应用程序的特定类别或对象。设计模式能使不稳定依赖于相对稳定、具体依赖于相对抽象，避免会引起麻烦的紧耦合，以增强软件设计面对并适应变化的能力。
>
> From [维基百科](https://zh.wikipedia.org/wiki/设计模式_(计算机))

## Why

### 为什么我们需要设计模式呢？

先来看看维基百科上对于JavaScript的描述

> **JavaScript**，一种高级编程语言，通过[解释执行](https://zh.wikipedia.org/w/index.php?title=%E8%A7%A3%E9%87%8A%E6%89%A7%E8%A1%8C&action=edit&redlink=1)，是一门[动态类型](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E7%B1%BB%E5%9E%8B)，[面向对象](https://zh.wikipedia.org/wiki/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)（[基于原型](https://zh.wikipedia.org/wiki/%E5%8E%9F%E5%9E%8B%E7%A8%8B%E5%BC%8F%E8%A8%AD%E8%A8%88)）的直译语言[[4\]](https://zh.wikipedia.org/wiki/JavaScript#cite_note-:0-4)。它已经由ECMA（欧洲电脑制造商协会）通过[ECMAScript](https://zh.wikipedia.org/wiki/ECMAScript)实现语言的标准化[[4\]](https://zh.wikipedia.org/wiki/JavaScript#cite_note-:0-4)。
>
> From [维基百科](https://zh.wikipedia.org/wiki/设计模式_(计算机))

这里有两个重点：**动态类型**，**基于原型**。

这两个特性决定了我们在JavaScript代码中可以随时更改JavaScript变量的类型，更改JavaScript 对象的原型。隐式的类型转换更是个巨坑。

如果说JavaScript在设计上到底有多少问题，我们用个图来说明一下

> 《js权威指南》减去《js good parts》剩下的都是缺陷
>
> From 知乎

![7d1702e714fceea12980a26945fd8bd4_b](http://ww4.sinaimg.cn/large/65e4f1e6gw1fa35vey6eyj20go09dwfq.jpg)

由于JavaScript在语言层面存在的诸多问题，所以在开发大型项目的时候对项目代码的控制显得力不从心。急需框架来辅助我们解决这个问题。所以各式各样的框架就被开发出来了。

可是框架太多，我们改如何选择呢？这时候设计模式就派上用场了。

下一篇文章中，将讲解JavaScript中常用的几种设计模式。

