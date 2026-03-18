# Airbnb JavaScript 代码规范

> GitHub: https://github.com/airbnb/javascript

---

## 目录

- [类型](#类型)
- [引用](#引用)
- [对象](#对象)
- [数组](#数组)
- [解构](#解构)
- [字符串](#字符串)
- [函数](#函数)
- [箭头函数](#箭头函数)
- [类与构造函数](#类与构造函数)
- [模块](#模块)
- [变量](#变量)
- [比较运算符](#比较运算符)
- [命名约定](#命名约定)
- [注释](#注释)
- [空白字符](#空白字符)
- [逗号与分号](#逗号与分号)

---

## 类型

### 基本类型

- `string`
- `number`
- `boolean`
- `null`
- `undefined`
- `symbol`
- `bigint`

```javascript
const foo = 1;
let bar = foo;
bar = 9;
console.log(foo, bar); // => 1, 9
```

### 复杂类型

- `object`
- `array`
- `function`

```javascript
const foo = [1, 2];
const bar = foo;
bar[0] = 9;
console.log(foo[0], bar[0]); // => 9, 9
```

---

## 引用

### 使用 const 声明

```javascript
// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;
```

### 使用 let 重新赋值

```javascript
// bad
var count = 1;
if (true) {
  count += 1;
}

// good
let count = 1;
if (true) {
  count += 1;
}
```

---

## 对象

### 使用字面量创建对象

```javascript
// bad
const item = new Object();

// good
const item = {};
```

### 使用对象方法简写

```javascript
// bad
const atom = {
  value: 1,
  addValue: function (value) {
    return atom.value + value;
  },
};

// good
const atom = {
  value: 1,
  addValue(value) {
    return atom.value + value;
  },
};
```

### 使用属性值简写

```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
  lukeSkywalker,
};
```

---

## 数组

### 使用字面量创建数组

```javascript
// bad
const items = new Array();

// good
const items = [];
```

### 使用展开运算符复制数组

```javascript
// bad
const len = items.length;
const itemsCopy = [];
for (let i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

---

## 解构

### 对象解构

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;
  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

### 数组解构

```javascript
const arr = [1, 2, 3, 4];
const [first, second] = arr;
```

---

## 字符串

### 使用单引号

```javascript
// bad
const name = "Capt. Janeway";

// good
const name = 'Capt. Janeway';
```

### 使用模板字符串

```javascript
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

---

## 函数

### 使用命名函数表达式

```javascript
// good
const foo = function bar() {
  // ...
};
```

### 使用剩余参数

```javascript
// bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

// good
function concatenateAll(...args) {
  return args.join('');
}
```

---

## 箭头函数

### 使用箭头函数

```javascript
// bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```

### 单参数省略括号

```javascript
// good
[1, 2, 3].map(x => x * x);
```

---

## 类与构造函数

### 使用 class

```javascript
// bad
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// good
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```

---

## 模块

### 使用 import/export

```javascript
// bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
module.exports = AirbnbStyleGuide.es6;

// good
import { es6 } from './AirbnbStyleGuide';
export default es6;
```

---

## 变量

### 使用 const/let

```javascript
// bad
superPower = new SuperPower();

// good
const superPower = new SuperPower();
```

### 每个变量单独声明

```javascript
// bad
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// good
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```

---

## 比较运算符

### 使用严格相等

```javascript
// bad
if (name !== '') {}

// good
if (name) {}
```

---

## 命名约定

### 避免单字母名称

```javascript
// bad
function q() {}

// good
function query() {}
```

### 使用驼峰命名法

```javascript
// bad
const OBJEcttsssss = {};
const this_is_my_object = {};

// good
const thisIsMyObject = {};
```

### 使用 PascalCase 命名类

```javascript
// good
class User {
  constructor(options) {
    this.name = options.name;
  }
}
```

---

## 注释

### 多行注释

```javascript
/**
 * make() returns a new element
 * based on the passed-in tag name
 */
function make(tag) {
  return element;
}
```

### 单行注释

```javascript
// is current tab
const active = true;
```

---

## 空白字符

### 使用 2 个空格缩进

```javascript
// good
function() {
∙∙const name;
}
```

### 大括号前放置空格

```javascript
// good
function test() {
  console.log('test');
}
```

---

## 逗号与分号

### 使用尾随逗号

```javascript
// good
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};
```

### 使用分号

```javascript
// good
(function () {
  const name = 'Skywalker';
  return name;
}());
```

---

## 参考资料

- [Airbnb JavaScript Style Guide (GitHub)](https://github.com/airbnb/javascript)

---

*本文档基于 Airbnb JavaScript Style Guide 整理*
