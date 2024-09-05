---
sidebar_position: 3
---

# 安全

[[toc]]

## 安全 Headers 快速参考

### 推荐用于所有网站的安全 Headers

#### Content Security Policy (CSP) - 内容安全策略

跨站点脚本 （XSS）是一种攻击，其中网站上的漏洞允许注入和执行恶意脚本。

`Content-Security-Policy` 提供了一个附加层，通过限制页面可以执行哪些脚本来缓解 XSS 攻击。

建议使用以下方法之一启用严格的 CSP：

- 如果在服务器上呈现 HTML 页面，请使用**基于 nonce 的严格 CSP**
- 如果您的 HTML 必须静态提供或缓存，例如，如果它是单页应用程序，请使用**基于哈希的严格 CSP**

基于 nonce 的严格 CSP：

```:no-line-numbers
Content-Security-Policy:
  script-src 'nonce-{RANDOM1}' 'strict-dynamic' https: 'unsafe-inline';
  object-src 'none';
  base-uri 'none';
```

基于哈希的严格 CSP：

```:no-line-numbers
Content-Security-Policy:
  script-src 'sha256-{HASH1}' 'sha256-{HASH2}' 'strict-dynamic' https: 'unsafe-inline';
  object-src 'none';
  base-uri 'none';
```

:::tip 参见
- [内容安全策略（CSP）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)
- [Content-Security-Policy](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Security-Policy)
:::

### 为处理敏感用户数据的网站推荐的安全 Headers

#### X-Content-Type-Options

当从域名提供恶意 HTML 文档时（例如，如果上传到照片服务的图像包含有效的 HTML 标记），某些浏览器会将其视为活动文档并允许它在应用程序上下文中执行脚本，从而导致跨站点脚本错误。

`X-Content-Type-Options: nosniff` 通过指示浏览器在给定响应的标头中设置的 MIME 类型是正确的来防止它。 建议为**所有资源使用 `Content-Type`**

```:no-line-numbers
X-Content-Type-Options: nosniff
Content-Type: text/html; charset=utf-8
```

:::tip 参见
- [X-Content-Type-Options](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Content-Type-Options)
:::

#### X-Frame-Options

如果恶意网站可以将网站作为 iframe 嵌入，这可能允许攻击者通过点击劫持来调用用户的意外操作。

`X-Frame-Options` 指示是否应允许浏览器在 `<frame>`、`<iframe>`、`<embed>` 或 `<object>` 中呈现页面。 建议**所有 HTML** 都发这个 Headers 来表明是否允许被其他网站嵌入。

```:no-line-numbers
X-Frame-Options: DENY
```

:::tip 参见
- [X-Frame-Options](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-Frame-Options)
:::

#### Cross-Origin Resource Policy (CORP) - 跨域资源策略

攻击者可以嵌入来自另一个来源的资源，例如来自您的站点，以通过利用基于 Web 的跨站点泄漏来了解有关它们的信息。

`Cross-Origin-Resource-Policy` 通过指示它可以加载的网站集来减轻这种风险。 标头采用以下三个值之一：`same-origin`, `same-site` 和 `cross-origin`。 建议**所有资源**都发送这个header，以表明它们是否允许被其他网站加载。


```:no-line-numbers
Cross-Origin-Resource-Policy: same-origin
```

:::tip 参见
- [Cross-Origin-Resource-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Resource-Policy)
:::

#### Cross-Origin Opener Policy (COOP)

攻击者的网站可以在弹出窗口中打开另一个站点，通过利用基于 Web 的跨站点泄漏来了解有关该站点的信息。

`Cross-Origin-Opener-Policy` 为文档提供了一种将自身与通过 `window.open()` 打开的跨源窗口或带有 `target="_blank"` 而没有 `rel="noopener"` 的链接隔离开的方法。因此，文档的任何跨域开启器都将无法引用它，也无法与之交互。

```:no-line-numbers
Cross-Origin-Opener-Policy: same-origin-allow-popups
```

:::tip 参见
- [Cross-Origin-Opener-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Opener-Policy)
:::

#### HTTP Strict Transport Security (HSTS)

通过普通 HTTP 连接的通信未加密，因此网络级窃听者可以访问传输的数据。

`Strict-Transport-Security` 通知浏览器它永远不应该使用 HTTP 加载站点，而是使用 HTTPS。设置后，浏览器将使用 HTTPS 而不是 HTTP 来访问，而无需在定义的持续时间内进行重定向。

```:no-line-numbers
Strict-Transport-Security: max-age=31536000
```

:::tip 参见
- [HTTP Strict Transport Security](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Strict-Transport-Security)
:::

### 具有高级功能的网站的安全 Headers

#### Cross-Origin Resource Sharing (CORS) - 跨域资源共享

与本节中的其他项目不同，跨域资源共享 (CORS) 不是 Headers，而是请求和允许访问跨域资源的浏览器机制。

默认情况下，浏览器强制执行同源策略以防止网页访问跨源资源。例如，当加载跨源图像时，即使它以视觉方式显示在网页上，页面上的 JavaScript 也无法访问图像的数据。资源提供者可以通过选择加入 CORS 来放宽限制并允许其他网站读取资源。

```:no-line-numbers
Access-Control-Allow-Origin: https://zydmall.com
Access-Control-Allow-Credentials: true
Access-Control-Allow-Methods: POST, GET, PUT, DELETE, OPTIONS
Access-Control-Allow-Headers: Authorization
Access-Control-Max-Age: 86400
```

:::tip 参见
- [Access-Control-Allow-Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)
- [Access-Control-Allow-Credentials](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)
- [Access-Control-Allow-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Headers)
- [Access-Control-Allow-Methods](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Methods)
- [Access-Control-Max-Age](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Max-Age)
:::

#### Cross-Origin Embedder Policy (COEP) - 跨源嵌入策略

默认情况下禁用 `SharedArrayBuffer` 或 `performance.measureUserAgentSpecificMemory()` 等功能。

`Cross-Origin-Embedder-Policy：require-corp` 阻止文档和 worker 加载跨源资源，例如图像、脚本、样式表、iframe 等，除非这些资源明确选择通过 CORS 或 CORP Headers 加载。 COEP 可以与 Cross-Origin-Opener-Policy 结合，将文档选择为跨域隔离。

当您想要为文档启用跨域隔离时，请使用 `Cross-Origin-Embedder-Policy: require-corp`。

```:no-line-numbers
Cross-Origin-Embedder-Policy: require-corp
```

:::tip 参见
- [Cross-Origin-Embedder-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Embedder-Policy)
:::

## 使用 HTTPS 安全连接

## 防止信息泄露

## 保护网站免受 XSS

### 使用 Trusted Types 防止基于 DOM 的跨站点脚本漏洞

基于 DOM 的跨站脚本 (DOM XSS) 是最常见的 Web 安全漏洞之一，并且很容易在应用程序中引入它。 [Trusted Types](https://developer.mozilla.org/en-US/docs/Web/API/Trusted_Types_API) 默认对危险的 Web API 函数加以保护，提供编写、安全审查和维护应用程序的工具，使其免受 DOM XSS 漏洞的影响。

:::warning
Chrome 83 支持 Trusted Types，其他浏览器可以使用 [polyfill](https://github.com/w3c/webappsec-trusted-types#polyfill)。 有关最新的跨浏览器支持信息，请参阅浏览器[兼容性](https://caniuse.com/mdn-api_trustedtypes)。
:::

Trusted Types 的工作原理是锁定以下有风险的接收器函数；

- **脚本操作：**[`<script src>`](https://developer.mozilla.org/docs/Web/HTML/Element/script#attr-src) 和设置 [`<script>`](https://developer.mozilla.org/docs/Web/HTML/Element/script) 元素的文本内容
- **从字符串生成 HTML：**[`innerHTML`](https://developer.mozilla.org/docs/Web/API/Element/innerHTML)、[`outerHTML`](https://developer.mozilla.org/docs/Web/API/Element/outerHTML)、[`insertAdjacentHTML`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe#attr-srcdoc)、[`<iframe> srcdoc`](https://developer.mozilla.org/docs/Web/HTML/Element/iframe#attr-srcdoc)、[`document.write`](https://developer.mozilla.org/docs/Web/API/Document/write)、[`document.writeln`](https://developer.mozilla.org/docs/Web/API/Document/writeln) 和 [`DOMParser.parseFromString`](https://developer.mozilla.org/docs/Web/API/DOMParser#DOMParser.parseFromString)
- **执行插件内容：**[`<embed src>`](https://developer.mozilla.org/docs/Web/HTML/Element/embed#attr-src)、[`<object data>`](https://developer.mozilla.org/docs/Web/HTML/Element/object#attr-data) 和 [`<object codebase>`](https://developer.mozilla.org/docs/Web/HTML/Element/object#attr-codebase)
- **运行时 JavaScript 代码编译：**`eval`、`setTimeout`、`setInterval`、`new Function()`

Trusted Types 要求您在将数据传递给上述接收器函数之前对其进行处理。仅使用字符串将失败，因为浏览器不知道数据是否可信：

:::danger 错误做法 👎
```js
Element.innerHTML  = location.href;
```
启用 Trusted Types 后，浏览器会抛出 *TypeError*，并阻止将 DOM XSS 接收器与字符串一起使用。
:::

要表示数据已被安全处理，请创建一个特殊对象 - Trusted Type。

:::tip 正确做法 👍
```js
Element.innerHTML  = TrustedHTML;
```
启用 Trusted Types 后，浏览器会抛出 *TypeError*，并阻止将 DOM XSS 接收器与字符串一起使用。
:::

Trusted Types 大大减小了应用程序的 DOM XSS 攻击面。它简化了安全审核，并允许您在浏览器中在运行时编译、lint 或捆绑代码时强制执行基于类型的安全检查。

#### 启用 Trusted Types

将以下 HTTP 响应标头添加到要迁移到 Trusted Types 的文档。

```
Content-Security-Policy: require-trusted-types-for 'script';
```

:::warning
Trusted Types 仅在 HTTPS 和 localhost 等安全上下文中可用。
:::

:::tip
大多数此类违规还可以通过对代码库运行代码 [eslint-plugin-no-unsanitized](https://github.com/mozilla/eslint-plugin-no-unsanitized) 来进行检测。这有助于快速识别大量违规。 也就是说，您还应该分析 CSP 违规，因为这些违规会在执行不合规的代码时触发。
:::

#### 修复 Trusted Type 违规

有几个选项用于修复 Trusted Type 违规。可以[重写违规代码](#重写违规代码)，[使用库](#使用库)，创建 Trusted Type 策略。

##### 重写违规代码

也许不再需要不符合标准的功能，或者可以在不使用容易出错的功能的情况下以现代方式重写？

:::danger
```js
el.innerHTML = '<img src=xyz.jpg>';
```
:::

:::tip
```js
el.textContent = '';
const img = document.createElement('img');
img.src = 'xyz.jpg';
el.appendChild(img);
```
:::

##### 使用库

一些库已经生成了可以传递给接收器函数的 Trusted Types。 例如，可以使用 [DOMPurify](https://github.com/cure53/DOMPurify) 清理 HTML 片段，删除 XSS。

```js
import DOMPurify from 'dompurify';
el.innerHTML = DOMPurify.sanitize(html, { RETURN_TRUSTED_TYPE: true });
```

DOMPurify 支持 Trusted Types，并将返回包装在 TrustedHTML 对象中的清理过的 HTML，这样浏览器就不会生成违规代码。

:::tip
推荐在 Vue 中使用 `v-html` 时使用此方案。
:::

##### 创建 Trusted Type 策略

有时，无法删除功能，并且没有库来清理值和创建 Trusted Type。在这种情况下，请自行创建 Trusted Type 对象。

```js
if (window.trustedTypes && trustedTypes.createPolicy) { // Feature testing
  const escapeHTMLPolicy = trustedTypes.createPolicy('myEscapePolicy', {
    createHTML: string => string.replace(/\</g, '<')
  });
}

const escaped = escapeHTMLPolicy.createHTML('<img src="x" onerror="alert(1)">');
console.log(escaped instanceof TrustedHTML);  // true
el.innerHTML = escaped;  // '<img src="x" onerror="alert(1)">'
```

此代码创建了一个名为 `myEscapePolicy` 的策略，该策略可以通过其 `createHTML()` 函数生成 [TrustedHTML](https://developer.mozilla.org/en-US/docs/Web/API/TrustedHTML) 对象。所定义的规则将对 `<` 字符进行 HTML 转义，以防止创建新的 HTML 元素。

:::tip
虽然传递给 `trustedTypes.createPolicy()` 的 JavaScript 函数 `createHTML()` 返回一个字符串，但 `createPolicy()` 返回一个策略对象，该对象将返回值包装为正确的类型（在本例中为 `TrustedHTML`）。
:::

### 使用严格的内容安全策略 (CSP) 缓解跨站点脚本 (XSS)

跨站脚本 (XSS)——将恶意脚本注入 Web 应用程序的能力——十多年来一直是最大的 Web 安全漏洞之一。

[内容安全策略 (CSP)](https://developer.mozilla.org/docs/Web/HTTP/CSP) 是一个附加的安全层，有助于缓解 XSS。 配置 CSP 涉及将 Content-Security-Policy HTTP 标头添加到网页并设置值以控制允许用户代理为该页面加载哪些资源。使用基于随机数或哈希的 CSP 来缓解 XSS，而不是常用的基于主机白名单的 CSP，后者通常会使页面暴露于 XSS，因为它们可以在大多数配置中被绕过。

:::tip 关键术语

**nonce**

nonce 是仅使用一次的随机数，可用于将 `<script>` 标签标记为可信。

**散列函数**

散列函数是一种数学函数，可将输入值转换为压缩数值——散列。 哈希（例如 SHA-256）可用于将内联 `<script>` 标签标记为可信。
:::

基于随机数或散列的内容安全策略通常称为**严格 CSP**。 当应用程序使用严格的 CSP 时，发现 HTML 注入漏洞的攻击者通常无法使用它们来强制浏览器在易受攻击的文档的上下文中执行恶意脚本。 这是因为严格的 CSP 只允许在服务器上生成散列脚本或具有正确 nonce 值的脚本，因此攻击者无法在不知道给定响应的正确 nonce 的情况下执行脚本。

:::tip
为了保护您的站点免受 XSS 攻击，请确保清理用户输入并将 CSP 用作额外的安全层。 CSP 是一种深度防御技术，可以防止恶意脚本的执行，但它不能替代避免（并及时修复）XSS 错误。
:::

白名单 CSP 在阻止攻击者利用 XSS 方面通常无效。 这就是为什么建议使用基于加密随机数或散列的严格 CSP 的原因，这样可以避免上述陷阱。


:::danger 白名单 CSP 👎
- 不能有效地保护您的网站。 ❌
- 必须高度定制。 😓
- 在大多数配置中可以绕过。😓
:::

:::tip 严格 CSP 👍
- 有效保护您的网站。 ✅
- 始终具有相同的结构。 😌
:::

严格的内容安全策略具有以下结构，并通过设置以下 HTTP 响应标头之一启用：

- **基于 nonce 的严格 CSP**

```:no-line-numbers
Content-Security-Policy:
  script-src 'nonce-{RANDOM}' 'strict-dynamic';
  object-src 'none';
  base-uri 'none';
```

![基于 nonce 的严格 CSP](security/assets/nonce-based-strict-csp.png?as=webp)

- **基于哈希的严格 CSP**

```:no-line-numbers
Content-Security-Policy:
  script-src 'sha256-{HASHED_INLINE_SCRIPT}' 'strict-dynamic';
  object-src 'none';
  base-uri 'none';
```

以下属性使 CSP 与上述“严格”类似，因此是安全的：

- 使用 nonce `nonce-{RANDOM}` 或散列 `sha256-{HASHED_INLINE_SCRIPT}` 来指示站点开发人员信任哪些 `<script>` 标签，并且应该允许在用户的浏览器中执行这些标签。
- 设置 [`'strict-dynamic'`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src#strict-dynamic) 以通过自动允许执行由已受信任的脚本创建的脚本来减少部署基于 nonce 或基于散列的 CSP 的工作量。 这也解除了对大多数第三方 JavaScript 库和小部件的使用的阻碍。
- 不基于 URL 允许列表，因此不受常见 CSP 绕过的影响。
- 阻止不受信任的内联脚本，如内联事件处理程序或 `javascript: URI`。
- 限制 `object-src` 禁用危险的插件，例如 Flash。
- 限制 `base-uri` 以阻止 `<base>` 标记的注入。 这可以防止攻击者更改从相对 URL 加载的脚本的位置。

:::tip
严格 CSP 的另一个优点是 CSP 始终具有相同的结构，并且不需要为您的应用程序定制。
:::

## 保护用户不被跟踪
