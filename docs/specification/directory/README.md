---
lang: zh-cmn-Hans-CN
title: 目录规范
description: 项目目录规范
---

# 目录规范

## 项目根目录

```:no-line-numbers
project/
├── dist/
├── public/
├── src/
│   └── ...
├── tests/
|   ├── e2e/
│   └── unit/
├── .browserslistrc
├── .editorconfig
├── .env.development
├── .env.production
├── .eslintignore
├── .eslintrc.js
├── .gitignore
├── .gitlab-ci.yml
├── .lighthouserc.js
├── babel.config.js
├── commitlint.config.js
├── jest.config.js
├── package.json
├── package-lock.json
├── stylelint.config.js
└── tsconfig.json
```

- `dist/`：项目构建结果
- `public/`：静态文件，不受 webpack 影响
- `src/`：项目源代码，见 [`src` 目录](#src-目录)
- `tests/`：测试源代码
  - `e2e/`：E2E 测试代码
  - `unit/`：单元测试代码
- `.browserslistrc`：Browserslist 配置文件，配置浏览器兼容性
- `.editorconfig`：编辑器配置
- `.env.development` `.env.production`：环境配置
- `.eslintignore`：忽略不需要 ESLint 检查的目录或文件
- `.eslintrc.js`：ESLint 配置
- `.gitignore`：忽略不需要 Git 提交的目录或文件
- `.gitlab-ci.yml`：Gitlab CI 配置
- `.lighthouserc.js`：lighthouse 检查配置，在 CI 环境下运行
- `babel.config.js`：Babel 配置
- `commitlint.config.js`：commitlint 配置
- `lint-staged.config.js`：lint-staged 配置
- `jest.config.js`：Jest 配置
- `package.json`
- `package-lock.json`
- `stylelint.config.js`：stylelint 配置
- `tsconfig.json`：TypeScript 配置
- `vue.config.json`：Vue CLI 配置

## `src` 目录

```:no-line-numbers
project/
└── src/
    ├── assets/
    ├── components/
    ├── composables/
    ├── directives/
    ├── layouts/
    ├── plugins/
    ├── router/
    ├── service/
    ├── store/
    ├── types/
    ├── utils/
    ├── views/
    ├── App.vue
    ├── main.ts
    ├── registerServiceWorker.ts
    └── shims-vue.d.ts
```

- `assets/`：静态文件目录（例如图片）
- `components/`：项目公共组件
- `composables/`：项目 Composition API
- `directives/`：项目公共指令
- `layouts/`：页面布局组件
- `plugins/`：Vue 全局插件
- `router/`：路由配置
- `services/`：HTTP 请求封装方法
- `store/`：Vuex 相关代码
- `types/`：公用 Types
- `utils/`：工具 JS 函数
- `views/`：页面组件
- `App.vue`：根组件
- `main.js`：页面入口文件
- `registerServiceWorker.ts`：PWA 相关代码
- `shims-vue.d.ts`：Vue Types

:::warning
在 Nuxt 项目中，配置 [`srcDir`](https://nuxtjs.org/docs/configuration-glossary/configuration-srcdir) 才可以把项目源代码放进 `src/` 目录

```js
// nuxt.config.js
export default {
  srcDir: 'src/'
}
```
:::

## 模块的导出

模块应该使用统一入口进行导出，以 `components/` 为例

目录结构，注意这里 `HelloWorld/` 下的 `assets/` 为组件私有资源，`components/` 为私有组件。我们会把 `components/index.ts` 作为统一的组件入口。

```:no-line-numbers
components/
├── HelloWorld/
|   ├── assets/
|   ├── components/
|   ├── HelloWorld.vue
|   └── index.ts
└── index.ts
```

先把 Vue 组件导出成模块：

```js
// components/HelloWorld/index.ts
import HelloWorld from './HelloWorld.vue'

export default HelloWorld;
```

在把模块导出成统一入口：

```js
// components/index.ts
export { default as HelloWorld } from './HelloWorld';
```

在页面组件中使用：

```vue
<script>
import { HelloWorld } from '@/components';

export default {
  components: {
    HelloWorld,
  },
};
</script>
```

这样做的好处是可以方便的管理和引用组件，无需再组件的使用过程中频繁的寻找组件的代码路径。由于 Webpack 已经支持 TreeShaking，这里无需过多的考虑性能优化的问题。
