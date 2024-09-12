---
sidebar_position: 1
---


# HTML 规范

:::warning
HTML Validate 规则参考 `html-validate:recommended`，但是由于需要整理的内容非常多，在开发过程中，仍以实际的 HTML Validate 检查为准。本章内容仅供参考
:::

## 规则一览

### 可用规则

| 规则                                                                                      | 来源                          | 描述                                                               |
|-----------------------------------------------------------------------------------------|-----------------------------|------------------------------------------------------------------|
| [`attr-delimiter`](https://html-validate.org/rules/attr-delimiter.html)                 | `html-validate:recommended` | 不允许属性键和值之间有空格                                                    |
| [`attr-spacing`](https://html-validate.org/rules/attr-spacing.html)                     | `html-validate:recommended` | 属性必须用空格（通常是常规空格）分隔                                               |
| [`close-attr`](https://html-validate.org/rules/close-attr.html)                         | `html-validate:recommended` | 不允许带有属性的结束标签                                                     |
| [`close-order`](https://html-validate.org/rules/close-order.html)                       | `html-validate:recommended` | 禁止以错误顺序关闭的元素                                                     |
| [`deprecated`](https://html-validate.org/rules/deprecated.html)                         | `html-validate:recommended` | 禁止使用已弃用的元素                                                       |
| [`deprecated-rule`](https://html-validate.org/rules/deprecated-rule.html)               | `html-validate:recommended` | 禁止使用已弃用的规则                                                       |
| [`doctype-html`](https://html-validate.org/rules/doctype-html.html)                     | `html-validate:recommended` | 使用 html5 文档类型（`<!DOCTYPE html>`）                                 |
| [`element-name`](https://html-validate.org/rules/element-name.html)                     | `html-validate:recommended` | 禁止无效的元素名称                                                        |
| [`meta-refresh`](https://html-validate.org/rules/meta-refresh.html)                     | `html-validate:recommended` | 元刷新（`<meta http-equiv="refresh" content="..">`）有 0 秒延迟           |
| [`no-conditional-comment`](https://html-validate.org/rules/no-conditional-comment.html) | `html-validate:recommended` | 禁止使用 IE 条件注释                                                     |
| [`no-deprecated-attr`](https://html-validate.org/rules/no-deprecated-attr.html)         | `html-validate:recommended` | 禁止使用已弃用的属性                                                       |
| [`no-dup-attr`](https://html-validate.org/rules/no-dup-attr.html)                       | `html-validate:recommended` | 不允许同一元素上使用重复的属性                                                  |
| [`no-dup-class`](https://html-validate.org/rules/no-dup-class.html)                     | `html-validate:recommended` | 不允许同一元素上使用重复的 class                                              |
| [`no-dup-id`](https://html-validate.org/rules/no-dup-id.html)                           | `html-validate:recommended` | 不允许同一元素上使用重复的 ID                                                 |
| [`no-raw-characters`](https://html-validate.org/rules/no-raw-characters.html)           | `html-validate:recommended` | 禁止使用未转义的特殊字符                                                     |
| [`no-redundant-for`](https://html-validate.org/rules/no-redundant-for.html)             | `html-validate:recommended` | 禁止对 `<label>` 使用冗余的 `for` 属性                                     |
| [`no-redundant-role`](https://html-validate.org/rules/no-redundant-role.html)           | `html-validate:recommended` | 禁止使用冗余 `role`                                                    |
| [`prefer-button`](https://html-validate.org/rules/prefer-button.html)                   | `html-validate:recommended` | 优先使用 `<button>` 代替 `<input tpye="button">`                       |
| [`prefer-tbody`](https://html-validate.org/rules/prefer-tbody.html)                     | `html-validate:recommended` | 优先使用 `<tbody>` 包裹 `<tr>`，在适用的情况下，它还应与 `<thead>` 和 `<tfoot>` 结合使用 |
| [`script-type`](https://html-validate.org/rules/script-type.html)                       | `html-validate:recommended` | `<script>` 元素 `type` 属性必须是有效类型（`type` 在脚本是 JavaScript 资源时省略该属性）  |
| [`tel-non-breaking`](https://html-validate.org/rules/tel-non-breaking.html)             | `html-validate:recommended` | 要求电话号码中的不间断字符                                                    |
| [`unrecognized-char-ref`](https://html-validate.org/rules/unrecognized-char-ref.html)   | `html-validate:recommended` | 禁止无法识别的 HTML 实体                                                  |
| [`valid-id`](https://html-validate.org/rules/valid-id.html)                             | `html-validate:recommended` | 要求 id 属性是有效的标识符                                                  |

### 内容模型

| 规则                                                                                                    | 来源                          | 描述                              |
|-------------------------------------------------------------------------------------------------------|-----------------------------|---------------------------------|
| [`attribute-allowed-values`](https://html-validate.org/rules/attribute-allowed-values.html)           | `html-validate:recommended` | 验证允许值的属性                        |
| [`element-permitted-content`](https://html-validate.org/rules/element-permitted-content.html)         | `html-validate:recommended` | 验证元素内容模型，某些元素只能使用特定的子元素         |
| [`element-permitted-occurrences`](https://html-validate.org/rules/element-permitted-occurrences.html) | `html-validate:recommended` | 验证元素内容模型，在给定的上下文中，某些元素只能使用固定的次数 |
| [`element-permitted-order`](https://html-validate.org/rules/element-permitted-order.html)             | `html-validate:recommended` | 验证元素内容模型，某些元素具有子元素必须使用的特定顺序     |
| [`element-required-attributes`](https://html-validate.org/rules/element-required-attributes.html)     | `html-validate:recommended` | 确保存在必需的属性                       |
| [`element-required-content`](https://html-validate.org/rules/element-required-content.html)           | `html-validate:recommended` | 确保某些元素具有必须存在某些子元素的              |
| [`input-attributes`](https://html-validate.org/rules/input-attributes.html)                           | `html-validate:recommended` | 验证 `<input>` 属性的使用              |
| [`no-multiple-main`](https://html-validate.org/rules/no-multiple-main.html)                           | `html-validate:recommended` | 不允许同一文档中有多个 `<main>` 元素         |
| [`script-element`](https://html-validate.org/rules/script-element.html)                               | `html-validate:recommended` | `<script>` 元素必须有结束标记            |
| [`void-content`](https://html-validate.org/rules/void-content.html)                                   | `html-validate:recommended` | 禁止带有内容的 void 元素                 |

### 可访问性

| 规则                                                                                            | 来源                          | 描述                                                                                                               |
|-----------------------------------------------------------------------------------------------|-----------------------------|------------------------------------------------------------------------------------------------------------------|
| [`aria-hidden-body`](https://html-validate.org/rules/aria-hidden-body.html)                   | `html-validate:recommended` | `<body>` 元素上不使用 `aria-hidden`                                                                                    |
| [`aria-label-misuse`](https://html-validate.org/rules/aria-label-misuse.html)                 | `html-validate:recommended` | 禁止 `aria-label` 滥用                                                                                               |
| [`empty-heading`](https://html-validate.org/rules/empty-heading.html)                         | `html-validate:recommended` | 标题（`h1`-`h6`）必须有文字内容                                                                                             |
| [`empty-title`](https://html-validate.org/rules/empty-title.html)                             | `html-validate:recommended` | 标题（`<title>`）必须有文字内容                                                                                             |
| [`multiple-labeled-controls`](https://html-validate.org/rules/multiple-labeled-controls.html) | `html-validate:recommended` | 禁止 `<label>` 与多个控件关联                                                                                             |
| [`no-autoplay`](https://html-validate.org/rules/no-autoplay.html)                             | `html-validate:recommended` | 禁止自动播放媒体元素                                                                                                       |
| [`prefer-native-element`](https://html-validate.org/rules/prefer-native-element.html)         | `html-validate:recommended` | 优先使用原生 HTML 元素而不是 `role`                                                                                         |
| [`text-content`](https://html-validate.org/rules/text-content.html)                           | `html-validate:recommended` | 元素必须具有有效文本（默认情况下，此规则验证 `<button>`）                                                                               |
| [`wcag/h30`](https://html-validate.org/rules/wcag/h30.html)                                   | `html-validate:recommended` | [WCAG 2.1 H30](https://www.w3.org/WAI/WCAG21/Techniques/html/H30)：每个 `<a>` 链接都有一个描述文本目的的文本，描述可能来自纯文本或来自带有替代文本的图像 |
| [`wcag/h32`](https://html-validate.org/rules/wcag/h32.html)                                   | `html-validate:recommended` | [WCAG 2.1 H32](https://www.w3.org/WAI/WCAG21/Techniques/html/H32)：每个 `<form>` 元素至少包含一个提交按钮，以允许用户以可预测的方式与表单进行交互   |
| [`wcag/h36`](https://html-validate.org/rules/wcag/h36.html)                                   | `html-validate:recommended` | [WCAG 2.1 H36](https://www.w3.org/WAI/WCAG21/Techniques/html/H36)：所有用作提交按钮的图像都具有使用该 `alt` 属性的文本描述                |
| [`wcag/h37`](https://html-validate.org/rules/wcag/h37.html)                                   | `html-validate:recommended` | [WCAG 2.1 H37](https://www.w3.org/WAI/WCAG21/Techniques/html/H37)：所有图像都有替代文本（`alt` 属性）                           |
| [`wcag/h67`](https://html-validate.org/rules/wcag/h67.html)                                   | `html-validate:recommended` | [WCAG 2.1 H67](https://www.w3.org/WAI/WCAG21/Techniques/html/H67)：装饰图像具有空 `alt` 文本 (`alt=""`) 或不存在 `title`       |
| [`wcag/h71`](https://html-validate.org/rules/wcag/h71.html)                                   | `html-validate:recommended` | [WCAG 2.1 H71](https://www.w3.org/WAI/WCAG21/Techniques/html/H71)：所有 `<fieldset>` 都有一个 `<legend>` 元素作为第一个子元素     |

### SEO

| 规则                                                               | 来源                          | 描述                        |
|------------------------------------------------------------------|-----------------------------|---------------------------|
| [`long-title`](https://html-validate.org/rules/long-title.html)  | `html-validate:recommended` | 标题（`<title>`）文字不能超过70个字符  |

### 风格

| 规则                                                                                        | 来源                          | 描述                |
|-------------------------------------------------------------------------------------------|-----------------------------|-------------------|
| [`attr-case`](https://html-validate.org/rules/attr-case.html)                             | `html-validate:recommended` | 属性名使用小写           |
| [`attr-quotes`](https://html-validate.org/rules/attr-quotes.html)                         | `html-validate:recommended` | 属性引号使用双引号         |
| [`attribute-boolean-style`](https://html-validate.org/rules/attribute-boolean-style.html) | `html-validate:recommended` | 布尔属性忽略属性值         |
| [`attribute-empty-style`](https://html-validate.org/rules/attribute-empty-style.html)     | `html-validate:recommended` | 空属性省略空字符串         |
| [`doctype-style`](https://html-validate.org/rules/doctype-style.html)                     | `html-validate:recommended` | 要求 DOCTYPE 使用大写   |
| [`element-case`](https://html-validate.org/rules/element-case.html)                       | `html-validate:recommended` | 元素名称使用小写          |
| [`no-implicit-close`](https://html-validate.org/rules/no-implicit-close.html)             | `html-validate:recommended` | 显式关闭元素            |
| [`no-inline-style`](https://html-validate.org/rules/no-inline-style.html)                 | `html-validate:recommended` | 禁止内联样式            |
| [`no-self-closing`](https://html-validate.org/rules/no-self-closing.html)                 | `html-validate:recommended` | 禁止自闭合元素           |
| [`no-trailing-whitespace`](https://html-validate.org/rules/no-trailing-whitespace.html)   | `html-validate:recommended` | 不允许在行尾出现尾随空格      |
| [`void-style`](https://html-validate.org/rules/void-style.html)                           | `html-validate:recommended` | 省略自闭标签来关闭 void 元素 |

### 文档

| 规则                                                                 | 来源                          | 描述                |
|--------------------------------------------------------------------|-----------------------------|-------------------|
| [`no-utf8-bom`](https://html-validate.org/rules/no-utf8-bom.html)  | `html-validate:recommended` | 禁止文档具有 UTF-8 BOM  |
