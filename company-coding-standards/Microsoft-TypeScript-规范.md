# Microsoft TypeScript 代码规范

> GitHub Wiki: https://github.com/microsoft/TypeScript/wiki/Coding-guidelines

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [类型使用](#类型使用)
- [注释](#注释)
- [编程实践](#编程实践)

---

## 命名规范

### 类和接口

- 使用 **PascalCase**

```typescript
// 正确
class HttpClient {}
interface UserService {}
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

- 使用 **UPPER_SNAKE_CASE** 或 **camelCase**

```typescript
// 正确
const MAX_RETRY_COUNT = 3;
const defaultTimeout = 5000;
```

### 私有成员

- 使用下划线前缀

```typescript
// 正确
class MyClass {
    private _name: string;

    private _internalMethod(): void {}
}
```

### 接口命名

- 不要使用 I 前缀

```typescript
// 错误
interface IUserService {}

// 正确
interface UserService {}
```

---

## 代码格式

### 缩进

- 使用 **4 个空格**

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

### 空格

- 运算符两侧加空格
- 逗号后加空格

```typescript
// 正确
const x = 1 + 2;
function foo(a: number, b: number): void {}
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

### 使用类型别名

```typescript
// 正确
type UserId = number;
type UserMap = Map<UserId, User>;
```

### 使用接口定义对象形状

```typescript
// 正确
interface User {
    id: number;
    name: string;
    email: string;
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

---

## 注释

### 文件注释

```typescript
/**
 * @fileoverview 文件描述
 * @author 作者名
 */
```

### 类注释

```typescript
/**
 * 用户服务类
 *
 * 提供用户相关的操作方法
 */
class UserService {}
```

### 方法注释

```typescript
/**
 * 根据ID 获取用户
 *
 * @param id - 用户ID
 * @returns 用户对象，如果不存在则返回 undefined
 */
public getUser(id: number): User | undefined {}
```

### 使用 JSDoc

```typescript
/**
 * 计算两个数的和
 * @param a - 第一个数
 * @param b - 第二个数
 * @returns 两数之和
 */
function add(a: number, b: number): number {
    return a + b;
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

// 错误
const name = user && user.profile && user.profile.name;
```

### 使用空值合并

```typescript
// 正确
const value = input ?? "default";

// 错误
const value = input || "default";
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

// 错误
const message = "Hello, " + name + "!";
```

---

## 参考资料

- [TypeScript Coding Guidelines (GitHub Wiki)](https://github.com/microsoft/TypeScript/wiki/Coding-guidelines)
- [TypeScript 官方文档](https://www.typescriptlang.org/docs/)

---

*本文档基于 Microsoft TypeScript Coding Guidelines 整理*
