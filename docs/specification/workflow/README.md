---
lang: zh-Hans
title: 工作流程
description: 页面的描述
---

# 工作流程

![工作流程](./workflow.png?as=webp)

## 流程

总体来说分两个阶段：

- 设计稿还原阶段：今年根据**UI验收**的环节新增加，主要做设计稿的还原和交互效果，侧重于 CSS
- 接口联调阶段：主要做前后端接口联调和交互逻辑，侧重于 JS 逻辑代码

### 设计稿还原阶段

- 分支名统一为 `preview`
- **每个页面完成**发起一次合并请求，由 @魏宏裕 审查代码
- 审查反馈大概于一个工作日内反馈完成，反馈内容在 Gitlab 合并请求的回复里
- 审查成功，则会交由 UI设计师 进行验收
- UI 验收完成前，**不允许联调接口**
- UI 验收完成后，会合并到版本分支

### 功能开发/联调阶段

- 分支名采用**版本号+团队名**，比如：`V2.2.5_20220429_qgu`
- **每天**发起一次合并请求（仅提交完成的部分），由 @魏宏裕 审查代码
- 审查反馈大概于一个工作日内反馈完成，反馈内容在 Gitlab 合并请求的回复里
- 审查成功，则会根据需要决定是否部署并提交测试

:::warning
注意在接口联调的过程中，不要让已经完成的 UI 发生明显的变化
:::

## 规范

### Git 要求

- Git 用户名使用中文，格式为**团队+姓名**，比如：博为_沈济颖，并带上可联系的邮箱（最好是企业邮箱）
- 提交信息格式会有 commitlint 校验，采用 [约定式提交](https://www.conventionalcommits.org/)
- 单次提交的内容需要完整，避免临时性的提交，可以使用 rebase 合并多次提交
- 擅长用 cherry-pick 合并分支
- 不允许直接将代码推送到 master、test、advance、preproduction、production 等分支

### 强制规范

- ESLint 校验通过
- stylelint 校验通过
- HTML Validate 校验通过

:::warning
**不允许修改配置文件**，ESLint 允许单行规则禁用，stylelint 允许单文件规则禁用。
如果在代码审查环节中，发现 ESLint 或 stylelint 校验不通过，**将强制代码审查为不通过**。
:::

### HTML 规范

- 优先使用语义化标签
- 擅长利用 HTML 属性优化用户体验
- 尽量减少 DOM 数量
- 避免在 HTML 中使用 `style` 属性

### CSS 规范

- 优先使用 [Tailwind CSS](https://tailwindcss.com/) 样式
- 优先使用 Flex 布局和 Grid 布局，避免滥用 Float 布局和 Position

### JS 规范

- 优先使用浏览器原生 API 实现各种功能，可用 [VueUse](https://vueuse.org/)
- 优先使用工具函数，如 [lodash](https://lodash.com/)、[date-fns](https://vueuse.org/)，避免重复发明轮子

### 图片规范

- 图像格式优先级：
  - 低彩图片：SVG > AVIF > WebP > PNG
  - 多彩图片：AVIF > WebP > JPG
- 必要时使用响应式图片
- 避免重设图片大小
- 避免图片出现 404

### 字体规范

- 不允许使用图标字体（Icon Font），使用 SVG 代替

### 媒体（视频/音频）规范

- 编码优先级：
  - AV1 > HEVC(H.265) > VP9 > VP8 > AVC(H.264) > Theora
- 格式优先级：
  - webm > ogv > mp4
- 编码优先于格式

### Vue/Nuxt 规范

- 优先使用 Composition API 语法
- 鼓励使用 TypeScript

### 功能性要求

- 登录鉴权机制，使用 [@nuxtjs/auth](https://auth.nuxtjs.org/)
- 对于金额计算，必须使用 [mathjs](https://mathjs.org/)，避免金额精度误差
- 兼容性要求，必要时做降级处理：
  - iOS 13+
  - Android Chrome 76+
  - 主流手机品牌：小米、vivo、OPPO、华为、一加 等
