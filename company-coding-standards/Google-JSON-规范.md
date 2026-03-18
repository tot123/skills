# Google JSON 代码规范

> 官方文档：https://google.github.io/styleguide/jsoncstyleguide.html

---

## 目录

- [基本规则](#基本规则)
- [命名规范](#命名规范)
- [数据结构](#数据结构)
- [最佳实践](#最佳实践)

---

## 基本规则

### 文件编码

- 使用 **UTF-8** 编码

### MIME 类型

- 使用 `application/json`

---

## 命名规范

### 属性名

- 使用 **camelCase**

```json
{
  "userName": "John",
  "itemCount": 10,
  "createdAt": "2024-01-01"
}
```

### 避免保留字

```json
// 错误
{
  "class": "User",
  "default": true,
  "private": false
}

// 正确
{
  "className": "User",
  "isDefault": true,
  "isPrivate": false
}
```

---

## 数据结构

### 对象结构

```json
{
  "apiVersion": "1.0",
  "context": "client-request-id",
  "id": "item-123",
  "data": {
    "items": [
      { "id": 1, "name": "Item 1" },
      { "id": 2, "name": "Item 2" }
    ],
    "totalItems": 2
  },
  "error": null
}
```

### 数组结构

```json
{
  "items": [
    { "id": 1, "name": "Item 1" },
    { "id": 2, "name": "Item 2" }
  ]
}
```

### 分页结构

```json
{
  "data": {
    "items": [],
    "currentPage": 1,
    "totalPages": 10,
    "totalItems": 100,
    "itemsPerPage": 10
  }
}
```

---

## 最佳实践

### 使用一致的日期格式

```json
{
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

### 使用 null 表示缺失值

```json
{
  "middleName": null,
  "phone": null
}
```

### 使用空数组而非 null

```json
// 正确
{
  "items": []
}

// 避免
{
  "items": null
}
```

### 错误响应结构

```json
{
  "error": {
    "code": 400,
    "message": "Invalid request",
    "errors": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ]
  }
}
```

---

## 参考资料

- [Google JSON Style Guide (官方)](https://google.github.io/styleguide/jsoncstyleguide.html)

---

*本文档基于 Google JSON Style Guide 整理*
