---
title: 1.7 关于离线与实时渲染
---

本章的最后，这里要特别说明一下关于离线渲染和实时渲染，以及它们在本书中各自的分量。

目前很多计算机图形学教材或资料都有区分实时渲染和离线渲染，甚至一些书直接以“实时”的字样来命名书籍，例如经典的图书《Real-Time Rendering》[cite b:rtr]等，另一些书则完全偏重于离线渲染，例如《Physically Based Rendering: From Theory to Implementation》[cite b:pbrt]。本书聚焦于当前工业中流行的一些全局光照技术的讨论，处于知识学习的角度，我们并不区分实时渲染和离线渲染，这有两点原因。

首先游戏引擎中大量使用离线渲染的技术，例如几乎所有关于预处理的部分都涉及离线渲染，为什么需要预处理，就是它们的计算非常耗时，既然是预处理的不占用实时渲染的时间，那么往往就容易选择使用最好的离线渲染技术来进行预处理计算，例如很多环境贴图及其他间接光照贴图都是通过光线追踪技术来计算的；在Unity中使用的Enlighten技术也是基于辐射度理论(Radiosity)来与计算环境之间的遮挡关系，这样的例子我们在本书也会看到很多，如果不理解离线渲染的一些技术，将很难透彻地掌握和理解实时渲染。

其次，也是最重要的，从自身知识积累的角度，我们完全不应该刻意让自己去选择离线或者实时渲染，我们应该追求的是掌握计算机图形学中各种理论知识。因为图像硬件和图形学技术都在不断发展，今天的离线渲染技术很可能就是明天的实时渲染技术，例如本章讨论的基于物理的渲染在2010年之前大都还只是用在电影产业等离线渲染领域，但是目前工业中一些一流的游戏引擎基本上都是基于物理渲染的了。

所以，本书基本上不考虑离线和实时的区别（比如本章讲述的一些Disney在电影产业中使用的技术，蒙特卡洛积分，光线追踪等技术目前都主要是离线渲染的范畴），而只考虑的是帮助读者构建更加完善和有用的计算机图形学知识结构体系。希望这样的一种写作思路是一种对读者更有价值的思路。
