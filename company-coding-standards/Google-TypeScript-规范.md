# Google TypeScript 代码规范

> 官方文档：https://google.github.io/styleguide/tsguide.html

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [类型使用](#类型使用)
- [编程实践](#编程实践)

---

## 命名规范

### 类和接口

- 使用 **PascalCase**

```typescript
// 正确
class HttpClient {}
interface UserService {}
type UserRole = 'admin' | 'user';
```

### 函数和方法

- 使用 **camelCase**

```typescript
// 正确
function getUserById(id: number): User {}
public calculateTotal(): number {}
```

### 变量和参数

- 使用 **camelCase**

```typescript
// 正确
const userName = "John";
let itemCount = 0;
function process(item: Item): void {}
```

### 常量

- 使用 **UPPER_SNAKE_CASE**

```typescript
// 正确
const MAX_RETRY_COUNT = 3;
const DEFAULT_TIMEOUT_MS = 5000;
```

### 枚举

- 枚举名：**PascalCase**
- 枚举值：**PascalCase**

```typescript
// 正确
enum HttpStatus {
  Ok = 200,
  NotFound = 404,
  InternalServerError = 500,
}
```

### 模块

- 文件名：**camelCase** 或 **kebab-case**

```typescript
// 正确
// userService.ts 或 user-service.ts
export class UserService {}
```

---

## 代码格式

### 缩进

- 使用 **2 个空格**

### 大括号

- 左大括号放在同一行

```typescript
// 正确
if (condition) {
  doSomething();
} else {
  doSomethingElse();
}
```

### 分号

- 使用分号

```typescript
// 正确
const x = 1;
doSomething();
```

---

## 类型使用

### 显式类型注解

- 公共 API 必须有类型注解

```typescript
// 正确
export function getUser(id: number): User | undefined {
  // ...
}

export class UserService {
  public getUser(id: number): User | undefined {
    // ...
  }
}
```

### 避免使用 any

```typescript
// 错误
function process(data: any): void {}

// 正确
function process(data: unknown): void {
  if (typeof data === "string") {
    // ...
  }
}
```

### 使用联合类型

```typescript
// 正确
type Status = "pending" | "approved" | "rejected";
type Result = Success | Error;
```

### 使用类型别名

```typescript
// 正确
type UserId = number;
type UserMap = Map<UserId, User>;
```

### 使用接口定义对象

```typescript
// 正确
interface User {
  id: number;
  name: string;
  email: string;
}
```

---

## 编程实践

### 使用 const 和 let

```typescript
// 正确
const MAX_COUNT = 100;
let counter = 0;

// 错误
var x = 1;
```

### 使用箭头函数

```typescript
// 正确
const doubled = numbers.map(n => n * 2);
const sum = numbers.reduce((a, b) => a + b, 0);
```

### 使用可选链

```typescript
// 正确
const name = user?.profile?.name;
```

### 使用空值合并

```typescript
// 正确
const value = input ?? "default";
```

### 使用解构

```typescript
// 正确
const { name, age } = user;
const [first, second] = items;
```

### 使用模板字符串

```typescript
// 正确
const message = `Hello, ${name}!`;
```

---

## 参考资料

- [Google TypeScript Style Guide (官方)](https://google.github.io/styleguide/tsguide.html)

---

*本文档基于 Google TypeScript Style Guide 整理*
