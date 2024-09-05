---
lang: zh-cmn-Hans-CN
title: HTTP 响应数据规范
---

# HTTP 响应数据规范

## 数据格式

| MySQL数据类型                                       | JSON 数据类型              | 备注                           |
|-------------------------------------------------|------------------------|------------------------------|
| `CHAR`                                          | `string`               |                              |
| `VARCHAR`                                       | `string`               |                              |
| `TEXT`                                          | `string`               |                              |
| `BINARY`/`VARBINARY`/`BLOB`                     |                        | 原则上不使用                       |
| `ENUM`                                          | `string`               |                              |
| `SET`                                           | `string` or `string[]` |                              |
| `INT`/`SMALLINT`/`TINYINT`/`MEDIUMINT`/`BIGINT` | `number`               | 超过 `9007199254740992` 则使用字符串 |
| `DECIMAL`                                       | `number`               |                              |
| `FLOAT`/`DOUBLE`                                | `number`               | 原则上不使用                       |
| `DATE`/`DATETIME`                               | `string`               |                              |
| `TIME`                                          | `string`               |                              |
| `YEAR`                                          | `string`               |                              |
| `TIMESTAMP`                                     | `number`               |                              |
| `JSON`                                          | `Object` or `any[]`    |                              |

### 字符串

#### `CHAR`

#### `VARCHAR`

#### `TEXT`

#### `BINARY`/`VARBINARY`/`BLOB`

#### `ENUM`

#### `SET`

### 数值

#### `INT`/`SMALLINT`/`TINYINT`/`MEDIUMINT`/`BIGINT`

#### `DECIMAL`

#### `FLOAT`/`DOUBLE`

### 时间日期

#### `DATE`/`DATETIME`

#### `TIME`

#### `YEAR`

#### `TIMESTAMP`

### `JSON`

## 特殊数据

### ID

### 外联数据

### 空数据

## 命名
