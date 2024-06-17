---
title: BEM命名规范
date: 2023-09-09
description: 
tags: []
---
> https://juejin.cn/post/7262638440482619447

BEM（Block, Element, Modifier）是一种前端编码规范，用于命名 HTML 和 CSS 中的类和选择器。它旨在提供一种一致的方式来组织和命名代码，使其易于理解、扩展和维护。

以下是 BEM 规范的基本原则：

- 块（Block） ：块是一个独立的可重用组件，它代表一个完整的实体。它是整个 BEM 结构中最高层级的部分，应该有一个唯一的类名。 示例：`.m-button` 、 `.m-navbar`

- 元素（Element） ：元素是块的组成部分，不能独立存在。它们依赖于块的上下文，并且有属于块的类名作为前缀。 示例：`.button__text` 、 `.navbar__item`

- 修饰符（Modifier） ：修饰符用于修改块或元素的外观、状态或行为。它们是可选的，可以单独使用或与块或元素的类名结合使用。 示例：`.m-button--large` 、 `.m-upload__item--active`
