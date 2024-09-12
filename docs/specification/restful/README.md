---
sidebar_position: 5
toc_min_heading_level: 2
toc_max_heading_level: 5
---

# RESTful API 规范

:::note
服务端 API 推荐使用以下语言和框架实现：

- OpenJDK 17 + [Spring Boot](https://spring.io/projects/spring-boot)
- Python + [Django](https://www.djangoproject.com/)
- PHP + [Laravel](https://laravel.com/)
:::

import TOCInline from '@theme/TOCInline';

<TOCInline toc={toc} />

## 基础约定

### 协议和域名

#### 协议

总是启用 **HTTPS 协议**

#### 域名

API 应该与前端页面部署在不同的域名

```
https://api.example.com/
```

#####  CORS 支持

服务端 API 与前端页面在不同域名时，应该使用 [CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS) 避免跨域。

::::details
跨域资源共享(CORS) 是一种机制，它使用额外的 HTTP 头来告诉浏览器  让运行在一个 origin (domain) 上的 Web 应用被准许访问来自不同源服务器上的指定的资源。当一个资源从与该资源本身所在的服务器不同的域、协议或端口请求一个资源时，资源会发起一个跨域 HTTP 请求。

出于安全原因，浏览器限制从脚本内发起的跨源 HTTP 请求。 例如，XMLHttpRequest 和 Fetch API 遵循同源策略。 这意味着使用这些 API 的 Web 应用程序只能从加载应用程序的同一个域请求 HTTP 资源，除非响应报文包含了正确CORS响应头。

跨域资源共享标准新增了一组 HTTP 首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源。另外，规范要求，对那些可能对服务器数据产生副作用的 HTTP 请求方法（特别是 GET 以外的 HTTP 请求，或者搭配某些 MIME 类型的 POST 请求），浏览器必须首先使用 OPTIONS 方法发起一个预检请求（preflight request），从而获知服务端是否允许该跨域请求。服务器确认允许之后，才发起实际的 HTTP 请求。在预检请求的返回中，服务器端也可以通知客户端，是否需要携带身份凭证（包括 Cookies 和 HTTP 认证相关数据）。

CORS 请求失败会产生错误，但是为了安全，在 JavaScript 代码层面是无法获知到底具体是哪里出了问题。你只能查看浏览器的控制台以得知具体是哪里出现了错误。

:::tip
- [HTTP访问控制（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)
- [Access-Control-Allow-Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Origin)
- [Access-Control-Allow-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Headers)
- [Access-Control-Expose-Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Expose-Headers)
- [Access-Control-Allow-Methods](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Methods)
- [Access-Control-Max-Age](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Max-Age)
- [Access-Control-Allow-Credentials](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)
:::
::::

### 路径

- 接口路径以 `/api` 或 `/{version}/api` 开头

:::tip 正面例子 👍
```:no-line-numbers
/api/product
/v7/api/product
```
:::

:::danger 反面例子 👎
```:no-line-numbers
/biz/product
/biz/api/product
```
:::

**注意：一个产品无论后端有多少个服务组成也应该只有一个 API 入口**

:::tip 正面例子 👍
```:no-line-numbers
/api/product
/api/order
```
:::

:::danger 反面例子 👎
```:no-line-numbers
/product-service/product
/order-service/order
```
:::

- 路径命名应该使用**中划线命名法**，而非驼峰命名法 或 下划线命名法

:::tip 正面例子 👍

中划线命名法

```:no-line-numbers
/api/product-categories
```
:::

:::danger 反面例子 👎

下划线命名法

```:no-line-numbers
/api/product_categories
```

驼峰命名法

```:no-line-numbers
/api/productCategories
```
:::

- 接口路径使用资源**名词而非动词**，比如 `/api/product` `/api/order`，**动作应由 HTTP Method 体现**，资源组可以进行逻辑嵌套。

:::tip 正面例子 👍
```:no-line-numbers
POST /api/product
```
:::

:::danger 反面例子 👎
```:no-line-numbers
POST /api/create-product
```
:::

- 接口设计面向开放接口，而非单纯前端业务

要求我们在给结构路径命名时候面向通用业务的开放接口，而非单纯前端业务。

以获取筛选表单中的任务字段下拉选项为例：

:::tip 正面例子 👍
```:no-line-numbers
/api/product
```
:::

:::danger 反面例子 👎
```:no-line-numbers
/api/product-with-select
```

虽然这个接口暂时只用在表单的下拉选择中，但是需要考虑的是在未来可能会被用在任意场景，因此应以更通用方式提供接口交由客户端自由组合
:::

### 身份认证

API 的身份认证应该使用 OAuth 2.0 框架。

```
Authorization: <type> <credentials>
```

:::tip
- [HTTP 身份验证](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Authentication)
:::

:::tip
服务端推荐使用 [Spring Security](https://spring.io/projects/spring-security) 实现
:::

#### 用户信息应使用身份认证获取，不依赖客户端id

:::tip 正面例子 👍
```http request:no-line-numbers
POST /api/user
Authorization: Bearer b25ed4f6b1ec69afea62dc248e52b8b24c090dbf3c07046bf8ff8a6b

{
  "nickname": "meiko"
}
```
:::

:::danger 反面例子 👎

```http request:no-line-numbers
POST /api/user

{
  "userId": "OjP9LDwma1bMA68x8kzBm",
  "nickname": "meiko"
}
```
:::

### 请求方法

规范使用 HTTP 方法，参见 [MDN Web Doc](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods)

| Methods                                                                      | 操作                        | 对应 SQL   | 示例路径         |
|------------------------------------------------------------------------------|---------------------------|----------|--------------|
| [`GET`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)       | 读取（Read）：从服务器获取列表数据       | `SELECT` | /product     |
| [`GET`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)       | 读取（Read）：从服务器获取单条数据       | `SELECT` | /product/:id |
| [`POST`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST)     | 创建（Create）：在服务器创建数据       | `INSERT` | /product     |
| [`PUT`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PUT)       | 更新（Update）：在服务器更新数据（所有字段） | `UPDATE` | /product/:id |
| [`PATCH`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PATCH)   | 更新（Update）：在服务器更新数据（部分字段） | `UPDATE` | /product/:id |
| [`DELETE`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) | 删除（Delete）：在服务器删除数据       | `DELETE` | /product/:id |

### Headers

规范使用 HTTP Headers，参见 [MDN Web Doc](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)

:::tip 正面例子 👍
```http request:no-line-numbers
POST /api/product
Authorization: Bearer b25ed4f6b1ec69afea62dc248e52b8b24c090dbf3c07046bf8ff8a6b
Content-Type: application/json
```
:::

:::danger 反面例子 👎
Headers 不是标准 HTTP Headers

```http request:no-line-numbers
POST /api/product
AuthType: sid
Client: pc_web
UserType: user
UserKey: param:key:loginInfo:zyd0214999218:WECHAT:b46bf79b
```
:::

### 安全约定

#### 永远不要信任用户输入，为所有参数进行有效性校验

对于前端，参数有效性校验避免无效的请求，减轻服务器负载，提升用户体验。但是对于后端，参数有效性校验可以有效避免恶意请求，避免无效数据的写入，对数据安全和数据一致性有重大保障。

**后端校验永远优选于前端校验**，推荐使用 [Hibernate Validator](https://hibernate.org/validator/) 进行后端校验。

#### 敏感字段

永远加密敏感字段，其中密码推荐使用 PBKDF2 算法加密，其他敏感字段使用 AES 加密。

:::warning 注意
密码仅限在请求时作为参数使用，响应参数不应该包含密码相关字段。在数据库，密码字段推荐使用 Bcrypt 算法 或者 PBKDF2 算法进行存储。
:::

:::tip 正面例子 👍
```json
{
  "name": "田野",
  "idNumber": "RKGJ2oqWrHUhbV0YggJhCU3lZOD5H3/+vR944hOozl4=",
  "password": "5wlvu+Ye7TC33MT3VKxU6neaTpPk5EvfuGs+8a7zRLc="
}
```
:::

:::danger 反面例子 👎
```json
{
  "name": "田野",
  "idNumber": "310000199511159999",
  "password": "meiko@xxx.com"
}
```
:::

#### 对自增 ID 进行 Hash

不要直接使用自增 ID，这会导致爬虫泛滥，并容易泄漏数据量，直接使用自增 ID 还容易引起暴力破解的风险。

推荐对自增 ID 进行 Hash（例如 YouTube 和 bilibili），可以隐藏真实的业务 ID，从而增加了攻击成本。建议参考 [Hashids](https://hashids.org/)。

:::tip 正面例子 👍
```json
{
  "id": "Zn8DxdXx5Z5VD51dwElom"
}
```
:::

:::danger 反面例子 👎
```json
{
  "id": 1
}
```
:::

## 响应

### HTTP 状态码

规范使用 HTTP 状态码，参见 [MDN Web Doc](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)

| Methods  | 状态码              |
|----------|------------------|
| `GET`    | `200 OK`         |
| `POST`   | `201 Created`    |
| `PUT`    | `200 OK`         |
| `PATCH`  | `200 OK`         |
| `DELETE` | `204 No Content` |

#### 成功状态码说明

| 状态码                                                                              | 说明                 | 使用场景                                                                                                                                 |
|----------------------------------------------------------------------------------|--------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| [`200 OK`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/200)         | 请求成功               | `GET`、`PUT` 和 `PATCH` 请求的响应                                                                                                          |
| [`201 Created`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/201)    | 请求已成功，并因此创建了一个新的资源 | `POST` 请求的响应                                                                                                                         |
| [`202 Accepted`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/202)   | 请求已经接收到，但还未响应，没有结果 | 用于高并发量的提交或者修改接口，前端需要长轮询获取真正的请求状态，API 通常需要使用 [RabbitMQ](https://www.rabbitmq.com/) 或者 [Apache Kafka](https://kafka.apache.org/) 等消息队列 |
| [`204 No Content`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/204) | 对于该请求没有响应可发送       | `DELETE` 请求的响应                                                                                                                       |

#### 错误状态码说明

| 状态码                                                                                          | 说明                           | 使用场景                                                                |
|----------------------------------------------------------------------------------------------|------------------------------|---------------------------------------------------------------------|
| [`400 Bad Request`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/400)            | 语义有误，当前请求无法被服务器理解 或者 请求参数有误  | 用于常见逻辑错误，如解析 JSON 出现错误 或者 注册时用户已存在                                  |
| [`401 Unauthorized`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/401)           | 当前请求需要用户验证                   | 用户未提供身份验证凭据，或者没有通过身份验证（未登录 或者 登录过期）                                 |
| [`403 Forbidden`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/403)              | 当前请求拒绝访问                     | 用户通过了身份验证，但是不具有访问资源所需的权限（已登录，但是没有该接口的访问权限）                          |
| [`404 Not Found`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/404)              | 当前请求的 URL 不存在                | API 没有此 URL 地址                                                      |
| [`405 Method Not Allowed`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/405)     | 当前请求的方法不被支持                  | 如 API 要求 POST，而客户端使用 GET                                            |
| [`406 Not Acceptable`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/406)         | 当前请求要求的返回格式不支持               | 如 API 返回 JSON，而客户端要求 XML                                            |
| [`413 Payload Too Large`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/413)      | 当前请求提交的实体数据大小超过了能够处理的范围      | 比如文件上传过大                                                            |
| [`414 URI Too Long`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/414)           | 当前请求的 URI 长度超过了服务器能够解释的长度    | 如 Query String 过长，或者一些安全攻击                                          |
| [`415 Unsupported Media Type`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/415) | 当前请求发送的实体格式服务端不支持            | 如 API 要求发送 JSON，而客户端发送 FormData                                     |
| [`422 Unprocessable Entity`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/422)   | 语义正确，但是服务器无法处理所包含的指令         | 用于提示表单校验错误信息                                                        |
| [`429 Too Many Requests`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/429)      | 在一定的时间内用户发送了太多的请求，即超出了“频次限制” | 用于限制用户短时间内的请求频率和预防 DDoS                                             |
| [`500 Internal Server Error`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/500)  | 服务器错误，包括了其他 5xx 状态码          | API 代码运行出现异常并未被正确处理，或者服务器已经宕机                                       |

### 响应格式

- 应该使用 JSON，避免使用 XML 或 其他数据格式

:::tip 正面例子 👍
```json
{
  "id": "GwW0bZAzm2qQE1wDKqope"
}
```
:::

:::danger 反面例子 👎

使用纯文本

```text
GwW0bZAzm2qQE1wDKqope
```

使用 XML

```xml
<product>
  <id>GwW0bZAzm2qQE1wDKqope</id>
</product>
```
:::

:::details
- [Accept](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept)
- [Content-Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type)

```
Accept: application/json
Content-Type: application/json
```
:::

- 前后端传输过程以标准 JSON 格式，避免反复正反序列化

:::tip 正面例子 👍
```json
{
  "data": [
    {
      "id": "zNBWQ4VrEeMKkmY4PgvaX",
      "name": "施耐德 iC65 微型断路器"
    },
    {
      "id": "zKLNwDGMm6qQRegxvBr5A",
      "name": "施耐德 EA9AN 微型断路器"
    }
  ]
}
```
:::

:::danger 反面例子 👎

```json
{
  "data": "[{\"id\": \"zNBWQ4VrEeMKkmY4PgvaX\",\"name\": \"施耐德 iC65 微型断路器\"},{\"id\": \"zKLNwDGMm6qQRegxvBr5A\",\"name\": \"施耐德 EA9AN 微型断路器\"}]"
}
```
:::

- **时间字段以 ISO 8601 格式返回：YYYY-MM-DDTHH:MM:SSZ**

:::tip 正面例子 👍
```json
{
  "date": "2022-07-03T23:01:36+08:00"
}
```
:::

:::danger 反面例子 👎

时间格式不符合 ISO 8601 格式

```json
{
  "date": "2022-07-03 23:01:36"
}
```

使用时间戳

```json
{
  "date": 1656860496
}
```
:::

- **空数组使用 `[]`，而不是 `null`**

:::tip 正面例子 👍
```json
{
  "list": []
}
```
:::

:::danger 反面例子 👎
```json
{
  "list": null
}
```
:::

### 统一错误响应

在接口处理发生错误的时候，如果是客户端请求参数导致的错误，会返回 `4xx` 状态码，如果是服务端的处理逻辑错误，会返回 `5xx` 状态码。所有的异常对象都是对这个异常状态的描述：

```json
{
  "error": "ValidationFailed",
  "message": "用户名不能为空",
  "details": [
    { "field": "title", "message": "required", "code": "MissingField" }
  ]
}
```

```typescript
interface Error {
  error: string;
  message: string;
  detail?: Object[];
}
```

:::danger 5xx 服务端错误
对于出现 `5xx` 服务端错误，可以在开发环境将服务器的错误信息返回，方便在开发中调试：

```json
// 开发环境
{
  "error": "InternalServerError",
  "message": "Failed to convert value of type 'java.lang.String' to required type 'java.lang.Integer'; nested exception is java.lang.NumberFormatException: For input string: \"4294967295\""
}
```

但是在生产环境中，绝对不要这么做！避免出现安全问题：

```json
// 生产环境
{
  "error": "InternalServerError",
  "message": ""
}
```

**注意：无论报错原因为何，凡是出现 `5xx` 服务端错误，客户端均不会做任何修改**
:::

| 参数        | 说明               |
|-----------|------------------|
| `error`   | **错误描述**，详见下表    |
| `message` | 错误提示信息，可用于前端界面提示 |
| `detail`  | （可选）导致错误的详细原因    |

#### 错误描述

:::warning TODO
此表格未完善
:::

| 值                     | 描述         |
|-----------------------|------------|
| `NoAccessRight`       | 缺少必要的权限    |
| `ValidationFailed`    | 参数中有值校验不通过 |
| `InternalServerError` | 服务端错误      |

## 查询类接口 - GET

| Methods | URL                                  | 说明         | 状态码      | 响应           |
|---------|--------------------------------------|------------|----------|--------------|
| `GET`   | `/api/product`                       | 查询所有数据     | `200 OK` | `Object[]`   |
| `GET`   | `/api/product?keyword=IC65`          | 带查询参数，查询数据 | `200 OK` | `Object[]`   |
| `GET`   | `/api/product?page=0&size=20`        | 带分页参数，查询数据 | `200 OK` | `Pagination` |
| `GET`   | `/api/product/2AE6RZd9wnmNdv7DLn0bd` | 查询指定详情数据   | `200 OK` | `Object`     |

```ts
interface PaginationMeta {
  pages: number;
  total: number;
}

interface Pagination {
  content: Object[];
  meta: PaginationMeta;
}
```

### 查询参数

查询类接口通常使用 QueryString 作为参数，通常在列表查询中使用

#### 固定查询参数

##### 分页

| 参数     | 说明                                    | 示例                 |
|--------|---------------------------------------|--------------------|
| `page` | 指定第几页，需要与`size`搭配使用，从 `0` 开始          | `?page=2&size=100` |
| `size` | 指定每页的记录数，需要与`page`搭配使用，**如不传此参数则不分页** | `?page=2&size=100` |

```:no-line-numbers
GET /api/product?page=0&size=100  # 查询第 1 页数据，每页 100 条
GET /api/product?page=2&size=100  # 查询第 3 页数据，每页 100 条
GET /api/product                  # 查询所有数据
```

##### 排序

| 参数       | 说明                            | 示例                       |
|----------|-------------------------------|--------------------------|
| `sortby` | 指定返回结果按照哪个属性排序，需要与`order`搭配使用 | `?sortby=name&order=asc` |
| `order`  | 排序顺序，需要与`sortby`搭配使用          | `?sortby=name&order=asc` |

```:no-line-numbers
GET /api/product?sortby=createdAt&order=asc   # 按 createdAt 字段升序排序
GET /api/product?sortby=updatedAt&order=desc  # 按 updatedAt 字段降序排序
```

##### 限制查询条数

| 参数       | 说明          | 示例           |
|----------|-------------|--------------|
| `limit`  | 指定返回记录的数量   | `?limit=10`  |
| `offset` | 指定返回记录的开始位置 | `?offset=10` |

```:no-line-numbers
GET /api/product?limit=10            # 查询 10 条数据
GET /api/product?limit=10&offset=10  # 查询 10 条数据，从第 10 条开始查询
```

##### 全文搜索

| 参数        | 说明                                                                                | 示例              |
|-----------|-----------------------------------------------------------------------------------|-----------------|
| `keyword` | 多列模糊查询，通常与全文搜索引擎（如 [ElasticSearch](https://www.elastic.co/cn/elasticsearch/)）搭配使用 | `?keyword=IC65` |

```:no-line-numbers
GET /api/product?keyword=IC65  # 查询任意字段中包含 IC65 关键词的数据
```

#### 非固定查询参数

##### ID

ID型数据使用**精确查询**，常用于外联字段，需要支持多个查询，**参数命名以`Ids`结尾**

```:no-line-numbers
GET /api/product?categoryIds=65     # 查询所有 categoryId 为 65 的数据
GET /api/product?categoryIds=65,97  # 查询所有 categoryId 为 65 或 97 的数据
```

##### 文本型

文本型数据使用**模糊查询**，**参数命名为字段名**

```:no-line-numbers
GET /api/product?name=IC65  # 查询所有 name 包含 IC65 的数据
```

##### 枚举

枚举型数据使用**精确查询**，需要支持多个查询，**参数命名为字段名**

```:no-line-numbers
GET /api/product?status=pending           # 查询所有 status 为 pending 的数据
GET /api/product?status=pending,complete  # 查询所有 status 为 pending 或 complete 的数据
```

##### 数值型

数值型数据，根据情况，使用**精确查询**和**区间查询**

- **精确查询**：**参数命名为字段名**
- **区间查询**：增加约定前缀
  - `gt`：大于
  - `gte`：大于等于
  - `lt`：小于
  - `lte`：小于等于

```:no-line-numbers
GET /api/product?stock=10                 # 查询所有 stock = 10 的数据

GET /api/product?gtStock=10               # 查询所有 stock > 10 的数据
GET /api/product?gteStock=10              # 查询所有 stock >= 10 的数据
GET /api/product?ltStock=10               # 查询所有 stock < 10 的数据
GET /api/product?lteStock=10              # 查询所有 stock <= 10 的数据

GET /api/product?gtStock=10&ltStock=20    # 查询所有 stock > 10 && stock < 20 的数据
GET /api/product?gteStock=10&lteStock=20  # 查询所有 stock >= 10 && stock <= 20 的数据
```

##### 时间/日期

时间/日期型字段，使用**区间查询**，以 `before` 和 `after` 作为前缀

```:no-line-numbers
# 查询所有 date 在 2022-07-04 13:00 ~ 2022-07-04 13:59 的数据（一小时）
GET /api/product?afterDate=2022-07-04T13:00:00+08:00&beforeDate=2022-07-04T13:59:59+08:00

# 查询所有 date 在 2022-07-04 的数据（一天）
GET /api/product?afterDate=2022-07-04T00:00:00+08:00&beforeDate=2022-07-04T23:59:59+08:00

# 查询所有 date 在 2022-07-03 ~ 2022-07-09 的数据（一周）
GET /api/product?afterDate=2022-07-03T00:00:00+08:00&beforeDate=2022-07-09T23:59:59+08:00

# 查询所有 date 在 2022-07-01 ~ 2022-07-31 的数据（一个月）
GET /api/product?afterDate=2022-07-01T00:00:00+08:00&beforeDate=2022-07-31T23:59:59+08:00

# 查询所有 date 在 2022-07-01 ~ 2022-09-30 的数据（一季度）
GET /api/product?afterDate=2022-07-01T00:00:00+08:00&beforeDate=2022-09-30T23:59:59+08:00

# 查询所有 date 在 2022-01-01 ~ 2022-12-31 的数据（一年）
GET /api/product?afterDate=2022-01-01T00:00:00+08:00&beforeDate=2022-12-31T23:59:59+08:00
```

### 查询类接口响应格式

#### 列表查询（分页）

```json
{
  "content": [
    {
      "id": "PrJ38xvJd5gLwrBxO9Y1A",
      "name": "施耐德 iC65 微型断路器",
      "stock": 10,
      "status": "sale",
      "createdAt": "2022-07-04T13:03:06+08:00"
    },
    {
      "id": "V0WJa4X26eygvwLZl9pom",
      "name": "施耐德 EA9AN 微型断路器",
      "stock": 10,
      "status": "inquiry",
      "createdAt": "2022-07-04T13:03:06+08:00"
    }
  ],
  "meta": {
    "pages": 10,
    "total": 10086
  }
}
```

#### 列表查询（不分页）

```json
[
  {
    "id": "PrJ38xvJd5gLwrBxO9Y1A",
    "name": "施耐德 iC65 微型断路器",
    "stock": 10,
    "status": "sale",
    "createdAt": "2022-07-04T13:03:06+08:00"
  },
  {
    "id": "V0WJa4X26eygvwLZl9pom",
    "name": "施耐德 EA9AN 微型断路器",
    "stock": 10,
    "status": "inquiry",
    "createdAt": "2022-07-04T13:03:06+08:00"
  }
]
```

#### 单条查询

```json
{
  "id": "PrJ38xvJd5gLwrBxO9Y1A",
  "name": "施耐德 iC65 微型断路器",
  "stock": 10,
  "status": "sale",
  "createdAt": "2022-07-04T13:03:06+08:00"
}
```

#### 注意事项

##### 所有数组需要返回一个`key`

:::tip 正面例子 👍
```json
{
  "list": [
    {
      "id": "OjP9LDwma52gR21x8kzBm",
      "name": "施耐德 iC65 微型断路器"
    },
    {
      "id": "JVny0D1v6G8Wqpe4d7XPR",
      "name": "施耐德 EA9AN 微型断路器"
    }
  ]
}
```
:::

:::danger 反面例子 👎
```json
{
  "list": [
    {
      "name": "施耐德 iC65 微型断路器"
    },
    {
      "name": "施耐德 EA9AN 微型断路器"
    }
  ]
}
```
:::

##### 可枚举字段使用有语义英文而非无语义数字

:::tip 正面例子 👍
```json
{
  "status": "pending"  // "pending" | "complete" | "error"
}
```
:::

:::danger 反面例子 👎
```json
{
  "status": 0
}
```
:::

##### 合理自然嵌套结构而不是平铺

对于外联数据，使用自然嵌套结构而不是平铺

:::tip 正面例子 👍
```json
{
  "id": "PrJ38xvJd5gLwrBxO9Y1A",
  "name": "施耐德 iC65 微型断路器",
  "categoryId": "1qWp840q2nPPy6kxJmyBn",
  "category": {
    "id": "1qWp840q2nPPy6kxJmyBn",
    "name": "微信断路器"
  }
}
```
:::

:::danger 反面例子 👎
```json
{
  "id": "PrJ38xvJd5gLwrBxO9Y1A",
  "name": "施耐德 iC65 微型断路器",
  "categoryId": "1qWp840q2nPPy6kxJmyBn",
  "categoryName": "微信断路器"
}
```
:::

## 创建类接口 - POST

### 请求参数

创建类接口参数使用 JSON 作为请求体，不应该使用 QueryString

:::tip 正面例子 👍
```http request:no-line-numbers
POST /api/user
Content-Type: application/json

{
  "username": "meiko",
  "password": "5wlvu+Ye7TC33MT3VKxU6neaTpPk5EvfuGs+8a7zRLc="
}
```
:::

:::danger 反面例子 👎
```http request:no-line-numbers
POST /api/user?username=meiko&password=5wlvu%2BYe7TC33MT3VKxU6neaTpPk5EvfuGs%2B8a7zRLc%3D
```
:::

### 创建类接口响应

| Methods | URL            | 说明   | 状态码           | 响应       |
|---------|----------------|------|---------------|----------|
| `POST`  | `/api/product` | 创建数据 | `201 Created` | `Object` |

创建完成后直接返回 ID

```json
{
  "id": "LjzXJx6k627PQNKZ2lN7B"
}
```

### 请求参数约束

#### 关联关系只以 `id` 为标识，其它字段不应依赖客户端

以创建用户为例：`POST /api/users`

:::tip 正面例子 👍
```json
{
  "username": "meiko",
  "password": "xxxx",
  "roleIds": [1, 2, 3]
}
```
:::

:::danger 反面例子 👎
```json
{
  "username": "meiko",
  "password": "xxxx",
  "roleIds": [
    {
      "id": 1,
      "name": "角色1"
    },
    {
      "id": 2,
      "name": "角色2"
    },
    {
      "id": 3,
      "name": "角色3"
    }
  ]
}
```
:::

## 更新类接口 - PUT/PATCH

| Methods | URL                                  | 说明           | 状态码      | 响应       |
|---------|--------------------------------------|--------------|----------|----------|
| `PUT`   | `/api/product/lkrdQx3Q6zNkRzeDRnv68` | 更新指定数据（所有字段） | `200 OK` | `Object` |
| `PATCH` | `/api/product/lkrdQx3Q6zNkRzeDRnv68` | 更新指定数据（部分字段） | `200 OK` | `Object` |

更新完成后直接返回 ID

```json
{
  "id": "lkrdQx3Q6zNkRzeDRnv68"
}
```

:::tip
总体来说，更新类接口与创建类接口很相似
:::

## 删除类接口 - DELETE

| Methods  | URL                                                            | 说明     | 状态码              | 响应  |
|----------|----------------------------------------------------------------|--------|------------------|-----|
| `DELETE` | `/api/product/dLEM04mVQavML57x8GV3q`                           | 删除单条数据 | `204 No Content` |     |
| `DELETE` | `/api/product?ids=dLEM04mVQavML57x8GV3q,W0dpVxlO6dlnQwb4Pav5q` | 批量删除数据 | `204 No Content` |     |

**删除接口应酌情提供批量删除**

例如 `DELETE /api/product/1` 表示删除 id 为 1 的数据

例如 `DELETE /api/product?ids=1,2,3` 表示批量删除 id 为 1 或 2 或 3 的数据

## 文件类接口

### 统一上传接口

| Methods | URL                   | 说明     | 状态码           | 响应       |
|---------|-----------------------|--------|---------------|----------|
| `POST`  | `/api/file`           | 上传文件   | `201 Created` | `File`   |
| `POST`  | `/api/multiple-files` | 批量上传文件 | `201 Created` | `File[]` |

```typescript
interface File {
  id: string;
  url: string;
  name: string;
}
```

| 参数     | 说明                    |
|--------|-----------------------|
| `id`   | 文件 ID，通常是文件的 checksum |
| `url`  | 文件在 CDN 或者 OSS 的 URL  |
| `name` | 原文件名                  |

:::warning 注意
上传接口的参数为 FormData，而非 JSON

```http request:no-line-numbers
POST /api/file
Content-Type: multipart/form-data
```
:::

#### 单个上传文件

```javascript
// 请求，注意这里是 FormData
{
  file: File
}
```

```json
// 响应
{
  "id": "ef7497affc2eedee5cb6fd58d8a86b310cc8d54a36c2569eb7c296e1af69efd5",
  "url": "https://cdn.example.com/upload/991b202e42d50c297d8785a40764e0df.pptx",
  "name": "nginx安装和配置指南.pptx"
}
```

#### 批量上传文件

```javascript
// 请求，注意这里是 FormData
{
  files: [File, File]
}
```

```json
// 响应
[
  {
    "id": "ef7497affc2eedee5cb6fd58d8a86b310cc8d54a36c2569eb7c296e1af69efd5",
    "url": "https://cdn.example.com/upload/991b202e42d50c297d8785a40764e0df.pptx",
    "name": "nginx安装和配置指南.pptx"
  },
  {
    "id": "da0651efdbce6b3cc06b3fb509177e7ab5d4c1b0e93b7a4d72acaad0cdf16152",
    "url": "https://cdn.example.com/upload/9fb3f25df4cf34e8fefe17be2d44fddd.pptx",
    "name": "前端入职培训.pptx"
  }
]
```

#### 注意事项

- 对于使用到文件的接口使用文件 id 或地址而非 FormData

:::tip 正面例子 👍
使用文件ID

```json
{
  "name": "施耐德 iC65 微型断路器",
  "fileId": "db93274594e9013a4190f068fabdfdbee5e9ccf8c02159439facb3bd51190bd2"
}
```

使用文件地址

```json
{
  "name": "施耐德 iC65 微型断路器",
  "fileUrl": "https://cdn.example.com/files/bb313c99.png"
}
```

**注意**：先由 `POST /api/file` 上传完文件拿到文件 id 或地址后再执行后续操作
:::

:::danger 反面例子 👎
```javascript
{
  name: "施耐德 iC65 微型断路器",
  file: File
}
```
:::

### 使用文件

- 文件路径至少补全至根路径

:::tip 正面例子 👍
补全至根路径

```json
{
  "data": {
    "id": "6GLj047k6RqKAnR4Qyq2A",
    "name": "施耐德 iC65 微型断路器",
    "avatar": "/upload/bb313c99.png"
  }
}
```

或者直接使用 CDN 或 OSS

```json
{
  "data": {
    "id": "6GLj047k6RqKAnR4Qyq2A",
    "name": "施耐德 iC65 微型断路器",
    "avatar": "https://cdn.example.com/files/bb313c99.png"
  }
}
```
:::

:::danger 反面例子 👎
```json
{
  "data": {
    "id": "6GLj047k6RqKAnR4Qyq2A",
    "name": "施耐德 iC65 微型断路器",
    "avatar": "bb313c99.png"
  }
}
```
:::

- 使用 CDN 或者 OSS 时，**要求使用 HTTPS 协议**

:::tip 正面例子 👍
```json
{
  "data": {
    "id": "QPXw3DE7r8YaK2gxWm78e",
    "name": "施耐德 iC65 微型断路器",
    "avatar": "https://cdn.example.com/files/bb313c99.png"
  }
}
```
:::

:::danger 反面例子 👎
```json
{
  "data": {
    "id": "QPXw3DE7r8YaK2gxWm78e",
    "name": "施耐德 iC65 微型断路器",
    "avatar": "http://cdn.example.com/files/bb313c99.png"
  }
}
```
:::

- **不要使用 CDN 或者 OSS 参数**，以便前端灵活处理

:::tip 正面例子 👍
```json
{
  "fileUrl": "https://cdn.example.com/files/bb313c99.png"
}
```
:::

:::danger 反面例子 👎
```json
{
  "fileUrl": "https://cdn.example.com/files/bb313c99.png?x-oss-process=style/s1"
}
```
:::

## 文档

文档推荐使用 [Spring REST Docs](https://spring.io/projects/spring-restdocs)
