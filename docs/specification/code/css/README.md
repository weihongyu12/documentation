---
lang: zh-cmn-Hans-CN
title: CSS规则
---

# stylelint 规则参考

:::warning
stylelint 规则参考 `stylelint-config-twbs-bootstrap`，但是由于需要整理的内容非常多，在开发过程中，仍以实际的 stylelint 检查为准。本章内容仅供参考
:::

## 规则一览

| 规则                                                                                                                                                  | 来源                                | 值                                   | 描述                                                    | Autofixable |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|-------------------------------------|-------------------------------------------------------|-------------|
| [`at-rule-no-unknown`](https://stylelint.io/user-guide/rules/list/at-rule-no-unknown)                                                               | `stylelint-config-recommended`    | `true`                              | 禁止未知 `@`规则                                            |             |
| [`block-no-empty`](https://stylelint.io/user-guide/rules/list/block-no-empty)                                                                       | `stylelint-config-recommended`    | `true`                              | 禁止空语句块                                                |             |
| [`color-no-invalid-hex`](https://stylelint.io/user-guide/rules/list/color-no-invalid-hex)                                                           | `stylelint-config-recommended`    | `true`                              | 禁止无效的十六进制（HEX）颜色                                      |             |
| [`comment-no-empty`](https://stylelint.io/user-guide/rules/list/comment-no-empty)                                                                   | `stylelint-config-recommended`    | `true`                              | 禁止空注释                                                 |             |
| [`custom-property-no-missing-var-function`](https://stylelint.io/user-guide/rules/list/custom-property-no-missing-var-function)                     | `stylelint-config-recommended`    | `true`                              | 不允许自定义属性缺少 `var` 函数                                   |             |
| [`declaration-block-no-duplicate-custom-properties`](https://stylelint.io/user-guide/rules/list/declaration-block-no-duplicate-custom-properties)   | `stylelint-config-recommended`    | `true`                              | 不允许在声明块中重复自定义属性                                       |             |
| [`declaration-block-no-duplicate-properties`](https://stylelint.io/user-guide/rules/list/declaration-block-no-duplicate-properties)                 | `stylelint-config-recommended`    | `true`                              | 禁止声明块中的重复属性                                           |             |
| [`declaration-block-no-shorthand-property-overrides`](https://stylelint.io/user-guide/rules/list/declaration-block-no-shorthand-property-overrides) | `stylelint-config-recommended`    | `true`                              | 禁止覆盖相关的速记属性的速记属性                                      |             |
| [`font-family-no-duplicate-names`](https://stylelint.io/user-guide/rules/list/font-family-no-duplicate-names)                                       | `stylelint-config-recommended`    | `true`                              | 禁止重复的字体系列（font-family）名称                              |             |
| [`font-family-no-missing-generic-family-keyword`](https://stylelint.io/user-guide/rules/list/font-family-no-missing-generic-family-keyword)         | `stylelint-config-recommended`    | `true`                              | 不允许在字体系列（font-family）名称列表中缺少通用系列                      |             |
| [`function-calc-no-unspaced-operator`](https://stylelint.io/user-guide/rules/list/function-calc-no-unspaced-operator)                               | `stylelint-config-recommended`    | `true`                              | 在 `calc` 函数中，在运算符之前，必须有一个空格或换行符加缩进；在运算符之后，必须有一个空格或换行符 |             |
| [`function-linear-gradient-no-nonstandard-direction`](https://stylelint.io/user-guide/rules/list/function-linear-gradient-no-nonstandard-direction) | `stylelint-config-recommended`    | `true`                              | 根据标准语法，不允许在 `linear-gradient()` 调用中使用无效的方向值           |             |
| [`keyframe-declaration-no-important`](https://stylelint.io/user-guide/rules/list/keyframe-declaration-no-important)                                 | `stylelint-config-recommended`    | `true`                              | 禁止在关键帧（keyframe）声明中使用 `!important`                    |             |
| [`media-feature-name-no-unknown`](https://stylelint.io/user-guide/rules/list/media-feature-name-no-unknown)                                         | `stylelint-config-recommended`    | `true`                              | 禁止未知媒体查询名称                                            |             |
| [`named-grid-areas-no-invalid`](https://stylelint.io/user-guide/rules/list/named-grid-areas-no-invalid)                                             | `stylelint-config-recommended`    | `true`                              | 禁止无效的命名网格区域                                           |             |
| [`no-descending-specificity`](https://stylelint.io/user-guide/rules/list/no-descending-specificity)                                                 | `stylelint-config-recommended`    | `true`                              | 不允许较低特异性的选择器出现在覆盖较高特异性的选择器之后                          |             |
| [`no-duplicate-at-import-rules`](https://stylelint.io/user-guide/rules/list/no-duplicate-at-import-rules)                                           | `stylelint-config-recommended`    | `true`                              | 禁止样式表中重复的 `@import` 规则                                |             |
| [`no-duplicate-selectors`](https://stylelint.io/user-guide/rules/list/no-duplicate-selectors)                                                       | `stylelint-config-recommended`    | `true`                              | 禁止样式表中的重复选择器                                          |             |
| [`no-empty-source`](https://stylelint.io/user-guide/rules/list/no-empty-source)                                                                     | `stylelint-config-recommended`    | `true`                              | 禁止空源代码                                                |             |
| [`no-extra-semicolons`](https://stylelint.io/user-guide/rules/list/no-extra-semicolons)                                                             | `stylelint-config-recommended`    | `true`                              | 不允许额外的分号                                              | 是           |
| [`no-invalid-double-slash-comments`](https://stylelint.io/user-guide/rules/list/no-invalid-double-slash-comments)                                   | `stylelint-config-recommended`    | `true`                              | 禁止 CSS 不支持的双斜线注释 (`//...`)                            |             |
| [`no-invalid-position-at-import-rule`](https://stylelint.io/user-guide/rules/list/no-invalid-position-at-import-rule)                               | `stylelint-config-recommended`    | `true`                              | 禁止样式表中的无效位置 `@import` 规则                              |             |
| [`property-no-unknown`](https://stylelint.io/user-guide/rules/list/property-no-unknown)                                                             | `stylelint-config-recommended`    | `true`                              | 禁止未知属性                                                |             |
| [`selector-pseudo-class-no-unknown`](https://stylelint.io/user-guide/rules/list/selector-pseudo-class-no-unknown)                                   | `stylelint-config-recommended`    | `true`                              | 禁止未知的伪类选择器                                            |             |
| [`selector-pseudo-element-no-unknown`](https://stylelint.io/user-guide/rules/list/selector-pseudo-element-no-unknown)                               | `stylelint-config-recommended`    | `true`                              | 禁止未知的伪元素选择器                                           |             |
| [`selector-type-no-unknown`](https://stylelint.io/user-guide/rules/list/selector-type-no-unknown)                                                   | `stylelint-config-recommended`    | `true`                              | 禁止未知类型选择器                                             |             |
| [`string-no-newline`](https://stylelint.io/user-guide/rules/list/string-no-newline)                                                                 | `stylelint-config-recommended`    | `true`                              | 禁止字符串中的（未转义的）换行符                                      |             |
| [`unit-no-unknown`](https://stylelint.io/user-guide/rules/list/unit-no-unknown)                                                                     | `stylelint-config-recommended`    | `true`                              | 禁止未知单位                                                |             |
| [`at-rule-name-case`](https://stylelint.io/user-guide/rules/list/at-rule-name-case)                                                                 | `stylelint-config-standard`       | `'lower'`                           | `@`规则名称指定小写                                           | 是           |
| [`at-rule-no-vendor-prefix`](https://stylelint.io/user-guide/rules/list/at-rule-no-vendor-prefix)                                                   | `stylelint-config-standard`       | `true`                              | 禁止在 `@` 规则使用浏览器前缀                                     | 是           |
| [`at-rule-semicolon-newline-after`](https://stylelint.io/user-guide/rules/list/at-rule-semicolon-newline-after)                                     | `stylelint-config-standard`       | `'always'`                          | 总是在 `@` 规则的分号后添加一个换行符                                 | 是           |
| [`block-closing-brace-newline-before`](https://stylelint.io/user-guide/rules/list/block-closing-brace-newline-before)                               | `stylelint-config-standard`       | `'always-multi-line'`               | 总是在多行块中的右大括号之前必须始终有一个换行符                              | 是           |
| [`block-closing-brace-space-before`](https://stylelint.io/user-guide/rules/list/block-closing-brace-space-before)                                   | `stylelint-config-standard`       | `'always-single-line'`              | 总是在单行块中的右大括号之前必须始终有一个空格                               | 是           |
| [`block-opening-brace-newline-after`](https://stylelint.io/user-guide/rules/list/block-opening-brace-newline-after)                                 | `stylelint-config-standard`       | `'always-multi-line'`               | 总是在多行块中的左大括号后必须始终有一个换行符                               | 是           |
| [`block-opening-brace-space-after`](https://stylelint.io/user-guide/rules/list/block-opening-brace-space-after)                                     | `stylelint-config-standard`       | `'always-single-line'`              | 总是在单行块中的左大括号后必须始终有一个空格                                | 是           |
| [`color-hex-case`](https://stylelint.io/user-guide/rules/list/color-hex-case)                                                                       | `stylelint-config-standard`       | `'lower'`                           | 为十六进制（HEX）颜色指定小写                                      | 是           |
| [`color-hex-length`](https://stylelint.io/user-guide/rules/list/color-hex-length)                                                                   | `stylelint-config-standard`       | `'short'`                           | 指定十六进制（HEX）颜色的简短表示法                                   | 是           |
| [`comment-empty-line-before`](https://stylelint.io/user-guide/rules/list/comment-empty-line-before)                                                 | `stylelint-config-standard`       | `'always'`                          | 总是在注释前要求空行                                            | 是           |
| [`comment-whitespace-inside`](https://stylelint.io/user-guide/rules/list/comment-whitespace-inside)                                                 | `stylelint-config-standard`       | `'always'`                          | 总是要求注释标记内部的空格                                         | 是           |
| [`custom-property-empty-line-before`](https://stylelint.io/user-guide/rules/list/custom-property-empty-line-before)                                 | `stylelint-config-standard`       | `'always'`                          | 在自定义属性之前要求空行                                          | 是           |
| [`custom-media-pattern`](https://stylelint.io/user-guide/rules/list/custom-media-pattern)                                                           | `stylelint-config-standard`       | `'^([a-z][a-z0-9]*)(-[a-z0-9]+)*$'` | 为自定义媒体查询名称指定中划线命名法（kebab-case）                        |             |
| [`declaration-bang-space-after`](https://stylelint.io/user-guide/rules/list/declaration-bang-space-after)                                           | `stylelint-config-standard`       | `'never'`                           | 感叹号后不允许空格                                             | 是           |
| [`declaration-bang-space-before`](https://stylelint.io/user-guide/rules/list/declaration-bang-space-before)                                         | `stylelint-config-standard`       | `'always'`                          | 感叹号前必须有一个空格                                           | 是           |
| [`declaration-block-semicolon-newline-after`](https://stylelint.io/user-guide/rules/list/declaration-block-semicolon-newline-after)                 | `stylelint-config-standard`       | `'always-multi-line'`               | 多行规则中分号后必须有换行符                                        | 是           |
| [`declaration-block-semicolon-space-after`](https://stylelint.io/user-guide/rules/list/declaration-block-semicolon-space-after)                     | `stylelint-config-standard`       | `'always-single-line'`              | 单行声明块中的分号后必须有一个空格                                     | 是           |
| [`declaration-block-single-line-max-declarations`](https://stylelint.io/user-guide/rules/list/declaration-block-single-line-max-declarations)       | `stylelint-config-standard`       | `1`                                 | 每一行只能有一个CSS属性                                         | 是           |
| [`declaration-block-trailing-semicolon`](https://stylelint.io/user-guide/rules/list/declaration-block-trailing-semicolon)                           | `stylelint-config-standard`       | `'always'`                          | 必须始终有一个尾随分号                                           | 是           |
| [`declaration-colon-newline-after`](https://stylelint.io/user-guide/rules/list/declaration-colon-newline-after)                                     | `stylelint-config-standard`       | `'always-multi-line'`               | 如果声明的值是多行的，则冒号后必须始终有一个换行符                             | 是           |
| [`declaration-colon-space-after`](https://stylelint.io/user-guide/rules/list/declaration-colon-space-after)                                         | `stylelint-config-standard`       | `'always-single-line'`              | 如果声明的值是单行的，冒号后必须有一个空格                                 | 是           |
| [`declaration-colon-space-before`](https://stylelint.io/user-guide/rules/list/declaration-colon-space-before)                                       | `stylelint-config-standard`       | `'never'`                           | 冒号前不能有空格                                              | 是           |
| [`font-family-name-quotes`](https://stylelint.io/user-guide/rules/list/font-family-name-quotes)                                                     | `stylelint-config-standard`       | `'always-where-recommended'`        | 尽在推荐规范时，为字体（`font-family`）增加引号                        |             |
| [`function-comma-newline-after`](https://stylelint.io/user-guide/rules/list/function-comma-newline-after)                                           | `stylelint-config-standard`       | `'always-multi-line'`               | 多行函数中逗号后必须有换行符                                        | 是           |
| [`function-comma-space-after`](https://stylelint.io/user-guide/rules/list/function-comma-space-after)                                               | `stylelint-config-standard`       | `'always-single-line'`              | 单行函数中逗号后必须有一个空格                                       | 是           |
| [`function-comma-space-before`](https://stylelint.io/user-guide/rules/list/function-comma-space-before)                                             | `stylelint-config-standard`       | `'never'`                           | 在函数的逗号前不允许有空格                                         | 是           |
| [`function-max-empty-lines`](https://stylelint.io/user-guide/rules/list/function-max-empty-lines)                                                   | `stylelint-config-standard`       | `0`                                 | 函数内不允许空行                                              | 是           |
| [`function-name-case`](https://stylelint.io/user-guide/rules/list/function-name-case)                                                               | `stylelint-config-standard`       | `'lower'`                           | 函数名必须是小写                                              | 是           |
| [`function-parentheses-newline-inside`](https://stylelint.io/user-guide/rules/list/function-parentheses-newline-inside)                             | `stylelint-config-standard`       | `'always-multi-line'`               | 多行函数的括号内必须始终有换行符                                      | 是           |
| [`function-parentheses-space-inside`](https://stylelint.io/user-guide/rules/list/function-parentheses-space-inside)                                 | `stylelint-config-standard`       | `'never-single-line'`               | 单行函数的括号内不能有空格                                         | 是           |
| [`function-url-quotes`](https://stylelint.io/user-guide/rules/list/function-url-quotes)                                                             | `stylelint-config-standard`       | `'always'`                          | `url` 函数必须使用引号                                        | 是           |
| [`function-whitespace-after`](https://stylelint.io/user-guide/rules/list/function-whitespace-after)                                                 | `stylelint-config-standard`       | `'always'`                          | 函数后总是使用空格                                             | 是           |
| [`indentation`](https://stylelint.io/user-guide/rules/list/indentation)                                                                             | `stylelint-config-standard`       | `2`                                 | 使用2空格缩进                                               | 是           |
| [`keyframes-name-pattern`](https://stylelint.io/user-guide/rules/list/keyframes-name-pattern)                                                       | `stylelint-config-standard`       | `'^([a-z][a-z0-9]*)(-[a-z0-9]+)*$'` | 关键帧名称（`@keyframes`）使用中划线命名（kebab-case）                |             |
| [`length-zero-no-unit`](https://stylelint.io/user-guide/rules/list/length-zero-no-unit)                                                             | `stylelint-config-standard`       | `true`                              | 不允许使用0长度的单位                                           | 是           |
| [`media-feature-colon-space-after`](https://stylelint.io/user-guide/rules/list/media-feature-colon-space-after)                                     | `stylelint-config-standard`       | `'always'`                          | 在媒体查询名称中的冒号后需要一个空格                                    | 是           |
| [`media-feature-colon-space-before`](https://stylelint.io/user-guide/rules/list/media-feature-colon-space-before)                                   | `stylelint-config-standard`       | `'never'`                           | 在媒体查询名称中的冒号前不允许有空格                                    | 是           |
| [`media-feature-name-case`](https://stylelint.io/user-guide/rules/list/media-feature-name-case)                                                     | `stylelint-config-standard`       | `'lower'`                           | 在媒体查询名称中总是使用小写                                        | 是           |
| [`media-feature-name-no-vendor-prefix`](https://stylelint.io/user-guide/rules/list/media-feature-name-no-vendor-prefix)                             | `stylelint-config-standard`       | `true`                              | 不允许媒查询名称使用浏览器前缀                                       | 是           |
| [`media-feature-parentheses-space-inside`](https://stylelint.io/user-guide/rules/list/media-feature-parentheses-space-inside)                       | `stylelint-config-standard`       | `'never'`                           | 在媒体查询的括号内不允许有空格                                       | 是           |
| [`media-feature-range-operator-space-after`](https://stylelint.io/user-guide/rules/list/media-feature-range-operator-space-after)                   | `stylelint-config-standard`       | `'always'`                          | 在媒体查询中的范围运算符之后需要一个空格                                  | 是           |
| [`media-feature-range-operator-space-before`](https://stylelint.io/user-guide/rules/list/media-feature-range-operator-space-before)                 | `stylelint-config-standard`       | `'always'`                          | 在媒体查询中的范围运算符之前需要一个空格                                  | 是           |
| [`media-query-list-comma-newline-after`](https://stylelint.io/user-guide/rules/list/media-query-list-comma-newline-after)                           | `stylelint-config-standard`       | `'always-multi-line'`               | 多行媒体查询列表中的逗号后必须始终有换行符                                 | 是           |
| [`media-query-list-comma-space-after`](https://stylelint.io/user-guide/rules/list/media-query-list-comma-space-after)                               | `stylelint-config-standard`       | `'always-single-line'`              | 单行媒体查询列表中的逗号后必须有一个空格                                  | 是           |
| [`media-query-list-comma-space-before`](https://stylelint.io/user-guide/rules/list/media-query-list-comma-space-before)                             | `stylelint-config-standard`       | `'never'`                           | 在媒体查询列表的逗号之前不允许有空格                                    | 是           |
| [`no-empty-first-line`](https://stylelint.io/user-guide/rules/list/no-empty-first-line)                                                             | `stylelint-config-standard`       | `true`                              | 不允许空的第一行                                              | 是           |
| [`no-eol-whitespace`](https://stylelint.io/user-guide/rules/list/no-eol-whitespace)                                                                 | `stylelint-config-standard`       | `true`                              | 禁止行尾空格                                                | 是           |
| [`no-irregular-whitespace`](https://stylelint.io/user-guide/rules/list/no-irregular-whitespace)                                                     | `stylelint-config-standard`       | `true`                              | 禁止不规则空格                                               | 是           |
| [`no-missing-end-of-source-newline`](https://stylelint.io/user-guide/rules/list/no-missing-end-of-source-newline)                                   | `stylelint-config-standard`       | `true`                              | 不允许源代码缺少结尾的换行符                                        | 是           |
| [`number-no-trailing-zeros`](https://stylelint.io/user-guide/rules/list/number-no-trailing-zeros)                                                   | `stylelint-config-standard`       | `true`                              | 不允许数字中的尾随零                                            | 是           |
| [`property-case`](https://stylelint.io/user-guide/rules/list/property-case)                                                                         | `stylelint-config-standard`       | `'lower'`                           | 属性使用小写                                                | 是           |
| [`property-no-vendor-prefix`](https://stylelint.io/user-guide/rules/list/property-no-vendor-prefix)                                                 | `stylelint-config-standard`       | `true`                              | 不允许属性的浏览器前缀                                           | 是           |
| [`selector-attribute-brackets-space-inside`](https://stylelint.io/user-guide/rules/list/selector-attribute-brackets-space-inside)                   | `stylelint-config-standard`       | `'never'`                           | 在属性选择器内的括号内不允许有空格                                     | 是           |
| [`selector-attribute-operator-space-after`](https://stylelint.io/user-guide/rules/list/selector-attribute-operator-space-after)                     | `stylelint-config-standard`       | `'never'`                           | 在属性选择器中的运算符后面不允许有空格                                   | 是           |
| [`selector-attribute-operator-space-before`](https://stylelint.io/user-guide/rules/list/selector-attribute-operator-space-before)                   | `stylelint-config-standard`       | `'never'`                           | 在属性选择器中的运前面不允许有空格                                     | 是           |
| [`selector-attribute-quotes`](https://stylelint.io/user-guide/rules/list/selector-attribute-quotes)                                                 | `stylelint-config-standard`       | `'always'`                          | 属性选择器总是为属性值加上引号                                       |             |
| [`selector-class-pattern`](https://stylelint.io/user-guide/rules/list/selector-class-pattern)                                                       | `stylelint-config-standard`       | `'^([a-z][a-z0-9]*)(-[a-z0-9]+)*$'` | class选择器使用中划线命名（kebab-case）                           |             |
| [`selector-combinator-space-after`](https://stylelint.io/user-guide/rules/list/selector-combinator-space-after)                                     | `stylelint-config-standard`       | `'always'`                          | 在选择器的组合符之后需要一个空格                                      | 是           |
| [`selector-combinator-space-before`](https://stylelint.io/user-guide/rules/list/selector-combinator-space-before)                                   | `stylelint-config-standard`       | `'always'`                          | 在选择器的组合符之前需要一个空格                                      | 是           |
| [`selector-descendant-combinator-no-non-space`](https://stylelint.io/user-guide/rules/list/selector-descendant-combinator-no-non-space)             | `stylelint-config-standard`       | `true`                              | 禁止选择器的后代组合符使用非空格字符                                    | 是           |
| [`selector-id-pattern`](https://stylelint.io/user-guide/rules/list/selector-id-pattern)                                                             | `stylelint-config-standard`       | `'^([a-z][a-z0-9]*)(-[a-z0-9]+)*$'` | ID选择器使用中划线命名（kebab-case）                              |             |
| [`selector-list-comma-newline-after`](https://stylelint.io/user-guide/rules/list/selector-list-comma-newline-after)                                 | `stylelint-config-standard`       | `'always'`                          | 选择器列表的逗号后需要换行符                                        | 是           |
| [`selector-max-empty-lines`](https://stylelint.io/user-guide/rules/list/selector-max-empty-lines)                                                   | `stylelint-config-standard`       | `0`                                 | 选择器中不允许空行                                             | 是           |
| [`selector-no-vendor-prefix`](https://stylelint.io/user-guide/rules/list/selector-no-vendor-prefix)                                                 | `stylelint-config-standard`       | `'true'`                            | 禁止选择器的浏览器前缀                                           | 是           |
| [`selector-pseudo-class-case`](https://stylelint.io/user-guide/rules/list/selector-pseudo-class-case)                                               | `stylelint-config-standard`       | `'lower'`                           | 伪类选择器总是使用小写                                           | 是           |
| [`selector-pseudo-class-parentheses-space-inside`](https://stylelint.io/user-guide/rules/list/selector-pseudo-class-parentheses-space-inside)       | `stylelint-config-standard`       | `'never'`                           | 在伪类选择器中的括号内不允许有空格                                     | 是           |
| [`selector-pseudo-element-case`](https://stylelint.io/user-guide/rules/list/selector-pseudo-element-case)                                           | `stylelint-config-standard`       | `'lower'`                           | 伪元素选择使用小写                                             | 是           |
| [`selector-pseudo-element-colon-notation`](https://stylelint.io/user-guide/rules/list/selector-pseudo-element-colon-notation)                       | `stylelint-config-standard`       | `'double'`                          | 为适用的伪元素使用双冒（`::`）表示法                                  | 是           |
| [`selector-type-case`](https://stylelint.io/user-guide/rules/list/selector-type-case)                                                               | `stylelint-config-standard`       | `'lower'`                           | 标签选择器总是使用小写                                           | 是           |
| [`shorthand-property-no-redundant-values`](https://stylelint.io/user-guide/rules/list/shorthand-property-no-redundant-values)                       | `stylelint-config-standard`       | `true`                              | 不允许速记属性中的冗余值                                          | 是           |
| [`string-quotes`](https://stylelint.io/user-guide/rules/list/string-quotes)                                                                         | `stylelint-config-standard`       | `'double'`                          | 在字符串使用双引号                                             | 是           |
| [`unit-case`](https://stylelint.io/user-guide/rules/list/unit-case)                                                                                 | `stylelint-config-standard`       | `'lower'`                           | 单位使用小写                                                | 是           |
| [`value-keyword-case`](https://stylelint.io/user-guide/rules/list/value-keyword-case)                                                               | `stylelint-config-standard`       | `'lower'`                           | 关键字值使用小写                                              | 是           |
| [`value-list-comma-space-before`](https://stylelint.io/user-guide/rules/list/value-list-comma-space-before)                                         | `stylelint-config-standard`       | `'never'`                           | 值列表的逗号前不允许有空格                                         | 是           |
| [`value-list-max-empty-lines`](https://stylelint.io/user-guide/rules/list/value-list-max-empty-lines)                                               | `stylelint-config-standard`       | `0`                                 | 值列表写在一行里（不分行）                                         | 是           |
| [`value-no-vendor-prefix`](https://stylelint.io/user-guide/rules/list/value-no-vendor-prefix)                                                       | `stylelint-config-standard`       | `true`                              | 不允许值的浏览器前缀                                            | 是           |
| [`at-rule-name-space-after`](https://stylelint.io/user-guide/rules/list/at-rule-name-space-after)                                                   | `stylelint-config-twbs-bootstrap` | `'always'`                          | 在`@`规则名称后需要一个空格                                       | 是           |
| [`at-rule-semicolon-space-before`](https://stylelint.io/user-guide/rules/list/at-rule-semicolon-space-before)                                       | `stylelint-config-twbs-bootstrap` | `'never'`                           | 在`@`规则的分号之前不允许空格                                      | 是           |
| [`color-named`](https://stylelint.io/user-guide/rules/list/color-named)                                                                             | `stylelint-config-twbs-bootstrap` | `'never'`                           | 禁止使用颜色关键字                                             |             |
| [`declaration-block-semicolon-newline-before`](https://stylelint.io/user-guide/rules/list/declaration-block-semicolon-newline-before)               | `stylelint-config-twbs-bootstrap` | `'never-multi-line'`                | 多行规则中的分号前不能有空格                                        |             |
| [`declaration-no-important`](https://stylelint.io/user-guide/rules/list/declaration-no-important)                                                   | `stylelint-config-twbs-bootstrap` | `true`                              | 在声明中禁止 `!important`                                   |             |
| [`font-weight-notation`](https://stylelint.io/user-guide/rules/list/font-weight-notation)                                                           | `stylelint-config-twbs-bootstrap` | `'numeric'`                         | `font-weight` 值必须始终是数字                                |             |
| [`function-url-no-scheme-relative`](https://stylelint.io/user-guide/rules/list/function-url-no-scheme-relative)                                     | `stylelint-config-twbs-bootstrap` | `true`                              | 禁止方案相对 url（`//`）                                      |             |
| [`max-empty-lines`](https://stylelint.io/user-guide/rules/list/max-empty-lines)                                                                     | `stylelint-config-twbs-bootstrap` | `2`                                 | 相邻空行最多两行                                              | 是           |
| [`number-leading-zero`](https://stylelint.io/user-guide/rules/list/number-leading-zero)                                                             | `stylelint-config-twbs-bootstrap` | `'never'`                           | 对于小于 1 的小数，不允许前导0                                     | 是           |
| [`selector-list-comma-newline-before`](https://stylelint.io/user-guide/rules/list/selector-list-comma-newline-before)                               | `stylelint-config-twbs-bootstrap` | `'never-multi-line'`                | 多行选择器列表中的逗号前不得有空格                                     | 是           |
| [`selector-list-comma-space-after`](https://stylelint.io/user-guide/rules/list/selector-list-comma-space-after)                                     | `stylelint-config-twbs-bootstrap` | `'always-single-line'`              | 单行选择器列表中的逗号后必须始终有一个空格                                 | 是           |
| [`selector-list-comma-space-before`](https://stylelint.io/user-guide/rules/list/selector-list-comma-space-before)                                   | `stylelint-config-twbs-bootstrap` | `'never-single-line'`               | 单行选择器列表中的逗号前不能有一个空格                                   | 是           |
| [`selector-max-attribute`](https://stylelint.io/user-guide/rules/list/selector-max-attribute)                                                       | `stylelint-config-twbs-bootstrap` | `2`                                 | 属性选择最多只能有2个属性                                         |             |
| [`selector-max-class`](https://stylelint.io/user-guide/rules/list/selector-max-class)                                                               | `stylelint-config-twbs-bootstrap` | `4`                                 | 类选择器，只允许嵌套4层                                          |             |
| [`selector-max-combinators`](https://stylelint.io/user-guide/rules/list/selector-max-combinators)                                                   | `stylelint-config-twbs-bootstrap` | `4`                                 | 组合选择器的只允许4层                                           |             |
| [`selector-max-compound-selectors`](https://stylelint.io/user-guide/rules/list/selector-max-compound-selectors)                                     | `stylelint-config-twbs-bootstrap` | `4`                                 | 复合选择器的只允许4层                                           |             |
| [`selector-max-id`](https://stylelint.io/user-guide/rules/list/selector-max-id)                                                                     | `stylelint-config-twbs-bootstrap` | `0`                                 | 不允许使用ID选择器                                            |             |
| [`selector-max-type`](https://stylelint.io/user-guide/rules/list/selector-max-type)                                                                 | `stylelint-config-twbs-bootstrap` | `2`                                 | 标签选择器只允许嵌套2层                                          |             |
| [`selector-max-universal`](https://stylelint.io/user-guide/rules/list/selector-max-universal)                                                       | `stylelint-config-twbs-bootstrap` | `1`                                 | 只允许使用1个通用选择器（`*`）                                     |             |
| [`selector-no-qualifying-type`](https://stylelint.io/user-guide/rules/list/selector-no-qualifying-type)                                             | `stylelint-config-twbs-bootstrap` | `true`                              | 不允许标签限定选择器                                            |             |
| [`unicode-bom`](https://stylelint.io/user-guide/rules/list/unicode-bom)                                                                             | `stylelint-config-twbs-bootstrap` | `'never'`                           | 禁止 Unicode 字节顺序标记                                     | 是           |
| [`value-list-comma-newline-after`](https://stylelint.io/user-guide/rules/list/value-list-comma-newline-after)                                       | `stylelint-config-twbs-bootstrap` | `'never-multi-line'`                | 多行值列表中的逗号后不得有空格                                       | 是           |
| [`value-list-comma-newline-before`](https://stylelint.io/user-guide/rules/list/value-list-comma-newline-before)                                     | `stylelint-config-twbs-bootstrap` | `'never-multi-line'`                | 多行值列表中的逗号前不得有空格                                       | 是           |
| [`value-list-comma-space-after`](https://stylelint.io/user-guide/rules/list/value-list-comma-space-after)                                           | `stylelint-config-twbs-bootstrap` | `'always'`                          | 值列表的逗号后需要一个空格                                         | 是           |

## 属性排序

### 全局

- [`all`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/all)

### 定位

- [`position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)
- [`inset`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/inset)
- [`inset-block`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/inset-block)
- [`inset-inline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/inset-inline)
- [`top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/top)
- [`right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/right)
- [`bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/bottom)
- [`left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/left)
- [`z-index`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/z-index)

### 显示模式

- [`box-sizing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-sizing)
- [`display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/display)

### Flex 布局

- [`flex`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex)
- [`flex-basis`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-basis)
- [`flex-direction`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-direction)
- [`flex-flow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-flow)
- [`flex-grow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-grow)
- [`flex-shrink`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-shrink)
- [`flex-wrap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-wrap)

### Grid 布局

- [`grid`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid)
- [`grid-area`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-area)
- [`grid-template`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-template)
- [`grid-template-areas`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-template-areas)
- [`grid-template-rows`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-template-rows)
- [`grid-template-columns`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-template-columns)
- [`grid-row`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-row)
- [`grid-row-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-row-start)
- [`grid-row-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-row-end)
- [`grid-column`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-column)
- [`grid-column-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-column-start)
- [`grid-column-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-column-end)
- [`grid-auto-rows`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-auto-rows)
- [`grid-auto-columns`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-auto-columns)
- [`grid-auto-flow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-auto-flow)
- [`grid-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-gap)
- [`grid-row-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-row-gap)
- [`grid-column-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-column-gap)

### Gap

- [`gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/gap)
- [`row-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/row-gap)
- [`column-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/column-gap)

### 布局对齐

- [`place-content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/place-content)
- [`place-items`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/place-items)
- [`place-self`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/place-self)
- [`align-content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/align-content)
- [`align-items`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/align-items)
- [`align-self`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/align-self)
- [`justify-content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-content)
- [`justify-items`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-items)
- [`justify-self`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-self)

### 排序

- [`order`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/order)

### 盒模型

- [`float`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/float)
- [`width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width)
- [`min-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/min-width)
- [`max-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/max-width)
- [`height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height)
- [`min-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/min-height)
- [`max-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/max-height)
- [`aspect-ratio`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/aspect-ratio)
- [`padding`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding)
- [`padding-block`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-block)
- [`padding-block-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-block-start)
- [`padding-block-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-block-end)
- [`padding-inline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-inline)
- [`padding-inline-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-inline-start)
- [`padding-inline-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-inline-end)
- [`padding-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-top)
- [`padding-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-right)
- [`padding-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-bottom)
- [`padding-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding-left)
- [`margin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin)
- [`margin-block`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-block)
- [`margin-block-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-block-start)
- [`margin-block-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-block-end)
- [`margin-inline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-inline)
- [`margin-inline-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-inline-start)
- [`margin-inline-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-inline-end)
- [`margin-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-top)
- [`margin-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-right)
- [`margin-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-bottom)
- [`margin-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin-left)
- [`overflow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow)
- [`overflow-x`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow-x)
- [`overflow-y`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow-y)
- [`-webkit-overflow-scrolling`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/-webkit-overflow-scrolling)
- ~~`-ms-overflow-x`~~
- ~~`-ms-overflow-y`~~
- `-ms-overflow-style`
- [`overscroll-behavior`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overscroll-behavior)
- [`overscroll-behavior-x`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overscroll-behavior-x)
- [`overscroll-behavior-y`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overscroll-behavior-y)
- [`overscroll-behavior-inline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overscroll-behavior-inline)
- [`overscroll-behavior-block`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overscroll-behavior-block)
- [`clip`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/clip)
- [`clip-path`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/clip-path)
- [`clear`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/clear)

### 排版

- [`font`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font)
- [`font-family`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-family)
- [`font-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size)
- [`font-variation-settings`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variation-settings)
- [`font-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-style)
- [`font-weight`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-weight)
- [`font-feature-settings`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-feature-settings)
- [`font-optical-sizing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-optical-sizing)
- [`font-kerning`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-kerning)
- [`font-variant`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant)
- [`font-variant-ligatures`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-ligatures)
- [`font-variant-caps`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-caps)
- [`font-variant-alternates`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-alternates)
- [`font-variant-numeric`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-numeric)
- [`font-variant-east-asian`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-east-asian)
- [`font-variant-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant-position)
- [`font-size-adjust`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size-adjust)
- [`font-stretch`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-stretch)
- [`font-effect`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-effect)
- [`font-emphasize`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-emphasize)
- [`font-emphasize-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-emphasize-position)
- [`font-emphasize-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-emphasize-style)
- `-webkit-font-smoothing`
- `-moz-osx-font-smoothing`
- [`font-smooth`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-smooth)
- [`hyphens`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/hyphens)
- [`line-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height)
- [`color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/color)
- [`text-align`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-align)
- [`text-align-last`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-align-last)
- [`text-emphasis`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-emphasis)
- [`text-emphasis-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-emphasis-color)
- [`text-emphasis-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-emphasis-style)
- [`text-emphasis-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-emphasis-position)
- [`text-decoration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration)
- [`text-decoration-line`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-line)
- [`text-decoration-thickness`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-thickness)
- [`text-decoration-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-style)
- [`text-decoration-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-color)
- [`text-underline-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-underline-position)
- [`text-underline-offset`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-underline-offset)
- [`text-indent`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-indent)
- [`text-justify`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-justify)
- [`text-outline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-outline)
- ~~`-ms-text-overflow`~~
- [`text-overflow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-overflow)
- [`text-overflow-ellipsis`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-overflow-ellipsis)
- [`text-overflow-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-overflow-mode)
- [`text-shadow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-shadow)
- [`text-transform`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-transform)
- [`text-wrap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-wrap)
- `-webkit-text-size-adjust`
- `-ms-text-size-adjust`
- [`letter-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/letter-spacing)
- [`word-break`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-break)
- [`word-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/word-spacing)
- ~~`word-wrap`~~ （`overflow-wrap` 的旧名称）
- [`overflow-wrap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow-wrap)
- [`tab-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/tab-size)
- [`white-space`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/white-space)
- [`vertical-align`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/vertical-align)

* [`list-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style)
* [`list-style-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style-position)
* [`list-style-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style-type)
* [`list-style-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style-image)

- [`src`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face/src)
- [`font-display`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face/font-display)
- [`unicode-range`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/unicode-range)
- [`size-adjust`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/size-adjust)
- [`ascent-override`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/ascent-override)
- [`descent-override`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/descent-override)
- [`line-gap-override`](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face/line-gap-override)

### 可访问性和交互

- [`pointer-events`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/pointer-events)
- ~~`-ms-touch-action`~~
- [`touch-action`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/touch-action)
- [`cursor`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor)
- [`visibility`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/visibility)
- [`zoom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/zoom)
- [`table-layout`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/table-layout)
- [`empty-cells`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/empty-cells)
- [`caption-side`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/caption-side)
- [`border-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-spacing)
- [`border-collapse`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-collapse)
- [`content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/content)
- [`quotes`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/quotes)
- [`counter-reset`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter-reset)
- [`counter-increment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/counter-increment)
- [`resize`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/resize)
- [`user-select`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/user-select)
- `nav-index`
- `nav-up`
- `nav-right`
- `nav-down`
- `nav-left`

### 背景和边框

- [`background`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background)
- [`background-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-color)
- [`background-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image)
- ~~`-ms-filter:\\'progid:DXImageTransform.Microsoft.gradient`~~
- ~~`filter:progid:DXImageTransform.Microsoft.gradient`~~
- ~~`filter:progid:DXImageTransform.Microsoft.AlphaImageLoader`~~
- [`filter`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter)
- [`background-repeat`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-repeat)
- [`background-attachment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-attachment)
- [`background-position`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position)
- [`background-position-x`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position-x)
- [`background-position-y`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-position-y)
- [`background-clip`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-clip)
- [`background-origin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-origin)
- [`background-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-size)
- [`background-blend-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-blend-mode)
- [`isolation`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/isolation)
- [`border`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border)
- [`border-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-color)
- [`border-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-style)
- [`border-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-width)
- [`border-block`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block)
- [`border-block-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-start)
- [`border-block-start-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-start-color)
- [`border-block-start-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-start-style)
- [`border-block-start-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-start-width)
- [`border-block-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-end)
- [`border-block-end-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-end-color)
- [`border-block-end-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-end-style)
- [`border-block-end-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-block-end-width)
- [`border-inline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline)
- [`border-inline-start`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-start)
- [`border-inline-start-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-start-color)
- [`border-inline-start-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-start-style)
- [`border-inline-start-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-start-width)
- [`border-inline-end`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-end)
- [`border-inline-end-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-end-color)
- [`border-inline-end-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-end-style)
- [`border-inline-end-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-inline-end-width)
- [`border-top`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top)
- [`border-top-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-color)
- [`border-top-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-style)
- [`border-top-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-width)
- [`border-right`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-right)
- [`border-right-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-right-color)
- [`border-right-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-right-style)
- [`border-right-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-right-width)
- [`border-bottom`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom)
- [`border-bottom-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom-color)
- [`border-bottom-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom-style)
- [`border-bottom-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom-width)
- [`border-left`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-left)
- [`border-left-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-left-color)
- [`border-left-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-left-style)
- [`border-left-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-left-width)
- [`border-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius)
- [`border-start-start-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-start-start-radius)
- [`border-start-end-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-start-end-radius)
- [`border-end-start-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-end-start-radius)
- [`border-end-end-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-end-end-radius)
- [`border-top-left-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-left-radius)
- [`border-top-right-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-top-right-radius)
- [`border-bottom-right-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom-right-radius)
- [`border-bottom-left-radius`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-bottom-left-radius)
- [`border-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image)
- [`border-image-source`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image-source)
- [`border-image-slice`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image-slice)
- [`border-image-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image-width)
- [`border-image-outset`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image-outset)
- [`border-image-repeat`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-image-repeat)
- [`outline`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/outline)
- [`outline-width`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/outline-width)
- [`outline-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/outline-style)
- [`outline-color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/outline-color)
- [`outline-offset`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/outline-offset)
- [`box-shadow`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow)
- [`mix-blend-mode`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/mix-blend-mode)
- ~~`filter:progid:DXImageTransform.Microsoft.Alpha(Opacity`~~
- ~~`-ms-filter:\\'progid:DXImageTransform.Microsoft.Alpha`~~
- [`opacity`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/opacity)
- ~~`-ms-interpolation-mode`~~

### SVG 属性

- [`alignment-baseline`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/alignment-baseline)
- [`baseline-shift`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/baseline-shift)
- [`dominant-baseline`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/dominant-baseline)
- [`text-anchor`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/text-anchor)
- [`word-spacing`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/word-spacing)
- [`writing-mode`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/writing-mode)

* [`fill`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/fill)
* [`fill-opacity`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/fill-opacity)
* [`fill-rule`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/fill-rule)
* [`stroke`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke)
* [`stroke-dasharray`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke-dasharray)
* [`stroke-dashoffset`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke-dashoffset)
* [`stroke-linecap`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke-linecap)
* [`stroke-linejoin`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke-linejoin)
* [`stroke-miterlimit`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke-miterlimit)
* [`stroke-opacity`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke-opacity)
* [`stroke-width`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stroke-width)

- [`color-interpolation`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/color-interpolation)
- [`color-interpolation-filters`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/color-interpolation-filters)
- [`color-profile`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/color-profile)
- [`color-rendering`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/color-rendering)
- [`flood-color`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/flood-color)
- [`flood-opacity`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/flood-opacity)
- [`image-rendering`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/image-rendering)
- [`lighting-color`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/lighting-color)
- [`marker-start`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/marker-start)
- [`marker-mid`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/marker-mid)
- [`marker-end`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/marker-end)
- [`mask`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/mask)
- [`shape-rendering`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/shape-rendering)
- [`stop-color`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stop-color)
- [`stop-opacity`](https://developer.mozilla.org/zh-CN/docs/Web/SVG/Attribute/stop-opacity)

### 过渡和动画

- [`transition`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)
- [`transition-delay`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-delay)
- [`transition-timing-function`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-timing-function)
- [`transition-duration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-duration)
- [`transition-property`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition-property)
- [`transform`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform)
- [`transform-origin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-origin)
- [`animation`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation)
- [`animation-name`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-name)
- [`animation-duration`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-duration)
- [`animation-play-state`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-play-state)
- [`animation-timing-function`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-timing-function)
- [`animation-delay`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-delay)
- [`animation-iteration-count`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-iteration-count)
- [`animation-direction`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-direction)
