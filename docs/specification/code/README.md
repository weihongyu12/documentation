---
lang: zh-cmn-Hans-CN
title: 代码规范
---

# 代码规范

## HTML

:::warning
HTML 目前可以暂时参照 [此规范](https://codeguide.bootcss.com/#html)，后续会根据实际需要进行调整。
:::

### 注重标签语义化

:::tip
HTML代码会使用 [`html-validate:recommended`](https://html-validate.org/) 进行检验，特别是 SSR 的场景下
:::

HTML 标签语义化是 Web 标准化的重要一环。也是标准定制时重要的设计原则。页面标签语义化的优点很明显，标签语义化是的诸如搜索引擎以及第三方内容抓取工具等更容易读懂页面代码。机器不会关注页面实际的渲染外观，只会关注页面内容本身，页面渲染的美观与否对机器识别毫无帮助。标签语义化也提高了页面代码的可读性，有利于代码阅读者理解代码对应的模块。

### 减少 DOM 结构

页面的 HTML 代码越多，整个页面维护起来就越难。同时还影响 DOM 的渲染。减少 DOM 结构，精简 HTML 代码以为了减少网络的传输，加快页面的渲染速度。通常可以通过以下方式达到精简 DOM 结构的目的：

- 删除多余的容器
- 使用 CSS 样式替代

### HTML Validate 规则参考

在项目中会使用 `html-validate:recommended` 作为 HTML 代码检查，点击这里可以查看详细的 [HTML 规则](/docs/specification/code/html)

## CSS

:::warning
CSS 和 Sass 将会使用 stylelint 进行代码检查，配置为 `stylelint-config-twbs-bootstrap`，由于 Bootstrap 没有提供文档参考，所以暂时使用 Airbnb CSS 文档，因此可能存在文档与实际校验规则不一致的情况，本段落可能根据配置进行更新。

CSS 目前可以暂时参照 [此规范](https://codeguide.bootcss.com/#css)，后续会根据实际需要进行调整。
:::

### 格式

- 使用 2 空格进行缩进
- 使用中划线命名(kebab-case)
  - 如果使用 BEM，下划线(snake_case)和大写开头(PascalCase)没问题
- 不要使用ID选择器
- 在规则声明中使用多个选择器时，为每个选择器指定一行
- 在规则声明之间放置空行
- `{` 在规则声明中的左大括号之前放置一个空格
- 在属性中，在 `:` 字符之后放置一个空格
- 将 `}` 规则声明的右大括号放在新行上

:::danger 反面例子 👎
```css
.avatar{
  border-radius:50%;
  border:2px solid white; }
.no, .nope, .not_good {
    /* ... */
}
#lol-no {
  /* ... */
}
```
:::

:::tip 正面例子 👍
```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  /* ... */
}
```
:::

### 注释

- 使用行注释而不是块注释。
- 在的行前进行注释。
- 避免行尾注释。
- 为特定用途的代码编写详细的注释：
  - z-index 的用途
  - 兼容性或特定于浏览器的 Hack 代码

:::danger 反面例子 👎
```css
/*
 * 块注释
 */
.avatar {
  border-radius: 50%; /* 行尾注释 */
  border: 2px solid white;
}
```
:::

:::tip 正面例子 👍
```css
/* 选择器行注释 */
.avatar {
  /* 属性行注释 */
  border-radius: 50%;
  border: 2px solid white;
}

```
:::

### OOCSS 和 BEM

出于以下原因，推荐鼓励 OOCSS 和 BEM：

- 有助于在 CSS 和 HTML 之间创建清晰、严格的关系
- 帮助我们创建可重用、可组合的组件
- 允许更少的嵌套和更低的特异性
- 有助于构建可扩展的样式表

**OOCSS**（Object Oriented CSS，面向对象 CSS），是一种编写 CSS 的方法，鼓励将样式表视为”对象“的集合：可在整个网站中独立使用的可重用、可重复的片段。

**BEM**（Block-Element-Modifier，块元素修饰符）是HTML 和 CSS 中类的命名约定。考虑到大型代码库和可扩展性，可以作为一套实现 OOCSS 的可靠指南。

:::tip 例子
```html
<article class="ListingCard ListingCard--featured">
  <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>
  <div class="ListingCard__content">
    <p>Vestibulum id ligula porta felis euismod semper.</p>
  </div>
</article>
```

```css
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

- `.ListingCard` 是“块（Block）”，代表更高级别的组件
- `.ListingCard__title` 是一个“元素（Element）”，代表 `.ListingCard` 的后代，有助于将块组合成一个整体
- `.ListingCard--featured` 是一个“修饰符（Modifier）”，代表 `.ListingCard` 块上的不同状态或变化
:::

:::tip
参见 [CSS-Tricks BEM 101](https://css-tricks.com/bem-101/)
:::

### stylelint 规则参考

在项目中会使用 `stylelint-config-twbs-bootstrap` 作为 CSS 代码检查，点击这里可以查看详细的 [CSS 规则](/docs/specification/code/css)

## Sass

### 语法

**使用 `.scss` 的语法，不使用 `.sass` 原本的语法**

:::tip
所有 Sass 代码也受到 `stylelint-config-twbs-bootstrap` 检查
:::

### 变量

变量名应使用破折号（例如 `$my-variable`）代替 camelCased 和 snake_cased 风格。对于仅用在当前文件的变量，可以在变量名之前添加下划线前缀（例如 `$_my-variable`）。

### 扩展指令

**应避免使用 `@extend` 指令**，因为它并不直观，而且具有潜在风险，特别是用在嵌套选择器的时候。即便是在顶层占位符选择器使用扩展，如果选择器的顺序最终会改变，也可能会导致问题。（比如，如果它们存在于其他文件，而加载顺序发生了变化）。其实，使用 @extend 所获得的大部分优化效果，gzip 压缩已经帮助你做到了，因此你只需要通过 mixin 让样式表更符合 DRY 原则就足够了。

### 嵌套选择器

**请不要让嵌套选择器的深度超过 3 层！**

:::danger 反面例子 👎
```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

当遇到以上情况的时候，CSS 大概是这样的：

- 与 HTML 强耦合的
- 过于具体
- 无法重用
:::

**永远不要嵌套 ID 选择器❗❗❗❗**

### stylelint 规则参考

在项目中会使用 `stylelint-config-twbs-bootstrap` 作为 Sass 代码检查，点击这里可以查看详细的 [Sass 规则](/docs/specification/code/sass)

## JavaScript

### Airbnb JavaScript 风格指南

**JS 代码规范采用 [Airbnb JavaScript 风格指南](https://airbnb.io/javascript/)**，请务必熟读

:::tip
所有 JS 代码都会使用 `eslint-config-airbnb-base` 进行强制检查
:::

- 参见：[Airbnb JavaScript 风格指南](https://airbnb.io/javascript/)

#### 核心思想

- 优先使用 ES6+ 语法
- 强类型编程
- 保持语法整洁和维护性

## TypeScript

TypeScript 目前并非强制要求，但是鼓励在项目中进行尝试。特别是对于公共函数、类这样的公共模块。

## Vue

### Vue 风格指南

**Vue 代码规范采用 [Vue 风格指南](https://v3.cn.vuejs.org/style-guide/)，级别是优先级C-推荐**，请务必熟读

:::tip
所有 Vue 文件都会使用 [`eslint-plugin-vue`](https://eslint.vuejs.org/) 进行强制检查，检查配置为 `plugin:vue/vue3-recommended`
:::

- 参见：[Vue 风格指南](https://v3.cn.vuejs.org/style-guide/)

#### 补充规则

##### 组件文件命名

单文件组件的文件名应该始终是单词大写开头 (PascalCase)

:::: details 例子
:::danger 反面例子 👎
```
components/
|- mycomponent.vue
```

```
components/
|- myComponent.vue
```

```
components/
|- my-component.vue
```
:::


:::tip 正面例子 👍
```
components/
|- MyComponent.vue
```

```
components/
|- MyComponent
   |- MyComponent.vue
   |- index.{js,ts}
```
:::
::::

##### 模板中的组件名大小写

模板中的组件名应该始终是单词是横线连接 (kebab-case)

:::: details 例子
:::danger 反面例子 👎
```vue
<!-- 不区分大小写 -->
<mycomponent />
```

```vue
<!-- camelCase -->
<myComponent />
```

```vue
<!-- PascalCase -->
<MyComponent />
```
:::


:::tip 正面例子 👍
```vue
<!-- kebab-case -->
<my-component />
```
:::
::::

##### 为组件样式设置 CSS Module

在项目组件内，应该使用 `module` 属性为 CSS 设置 CSS 作用域

> Why? `scoped` 属性最终生成的结果，是通过属性选择器的方式来避免 CSS 样式名的冲突，属性选择器的效率不如 class 选择器的效率高（特别是有大量节点的时候）。CSS Module 同样可以做到避免样式名冲突，它会生成一个全局唯一的样式名。同时，CSS Module 是可以在 Vue 组件的 JS 代码里被访问的。

:::: details 例子
:::danger 反面例子 👎
```vue
<template>
  <button class="btn btn-close">X</button>
</template>

<!-- 不使用 `scoped` 属性 和 CSS Module -->
<style>
.btn-close {
  background-color: red;
}
</style>
```

```vue
<template>
  <button class="button button-close">X</button>
</template>

<!-- 使用 `scoped` 属性 -->
<style scoped>
.button {
  border: none;
  border-radius: 2px;
}

.button-close {
  background-color: red;
}
</style>
```
:::

:::tip 正面例子 👍
```vue
<template>
  <button :class="[$style.button, $style.buttonClose]">X</button>
</template>

<!-- 使用 CSS Modules -->
<style module>
.button {
  border: none;
  border-radius: 2px;
}

.buttonClose {
  background-color: red;
}
</style>
```

```vue
<template>
  <button :class="[$style['c-Button'], $style['c-Button--close']]">X</button>
</template>

<!-- 使用 BEM 约定 -->
<style module>
.c-Button {
  border: none;
  border-radius: 2px;
}

.c-Button--close {
  background-color: red;
}
</style>
```
:::
::::
