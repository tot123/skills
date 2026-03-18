# Google JavaScript 代码规范

> 官方文档：https://google.github.io/styleguide/jsguide.html

---

## 目录

- [代码格式](#代码格式)
- [命名规范](#命名规范)
- [注释](#注释)
- [语言特性](#语言特性)
- [编程实践](#编程实践)

---

## 代码格式

### 行长度

- 最大行长度：**80** 个字符
- 例外：URL、命令行参数、长路径

### 缩进

- 使用 **2 个空格**
- 不要使用 Tab

### 大括号

- **K&R 风格**：左大括号放在同一行

```javascript
// 正确
if (condition) {
  doSomething();
} else {
  doSomethingElse();
}
```

### 语句终止

- 使用 **分号** 终止语句

```javascript
// 正确
const x = 1;
doSomething();
```

---

## 命名规范

### 类和构造函数

- 使用 **PascalCase**（大驼峰命名法）

```javascript
class MyClass {}
function MyConstructor() {}
```

### 函数和方法

- 使用 **camelCase**（小驼峰命名法）

```javascript
function doSomething() {}
```

### 变量

- 使用 **camelCase**（小驼峰命名法）

```javascript
const myVariable = 1;
let userName = 'John';
```

### 常量

- 使用 **UPPER_SNAKE_CASE**

```javascript
const MAX_ITEMS = 100;
const DEFAULT_TIMEOUT = 5000;
```

---

## 注释

### 文件注释

```javascript
/**
 * @fileoverview 文件描述
 * @author 作者名
 */
```

### 方法注释

```javascript
/**
 * 方法概述。
 *
 * @param {string} param1 - 参数描述
 * @returns {boolean} 返回值描述
 */
function myMethod(param1) {}
```

---

## 语言特性

### 变量声明

- 优先使用 `const`
- 需要重新赋值时使用 `let`
- 不要使用 `var`

```javascript
const x = 1;
let y = 2;
```

### 箭头函数

```javascript
const add = (a, b) => a + b;
arr.map(x => x * 2);
```

### 模板字符串

```javascript
const message = `Hello, ${name}!`;
```

---

## 编程实践

### 使用严格相等

```javascript
if (value === 'foo') {}
if (value !== null) {}
```

### 使用可选链

```javascript
const name = user?.profile?.name;
```

---

## 参考资料

- [Google JavaScript Style Guide (官方)](https://google.github.io/styleguide/jsguide.html)

---

*本文档基于 Google JavaScript Style Guide 整理*
