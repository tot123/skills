# Google Java 代码规范

> 官方文档：https://google.github.io/styleguide/javaguide.html

---

## 目录

- [源文件基础](#源文件基础)
- [代码格式](#代码格式)
- [命名规范](#命名规范)
- [注释](#注释)
- [编程实践](#编程实践)

---

## 源文件基础

### 文件编码

- 使用 **UTF-8** 编码

### 文件结构

```java
// 1. 许可证或版权声明
// 2. package 语句
// 3. import 语句
// 4. 顶级类声明
```

### 导入

- 不要使用通配符导入
- 导入顺序：
  1. `java.*`
  2. `javax.*`
  3. 第三方库
  4. 本地包

```java
import java.util.List;
import java.util.Map;

import javax.annotation.Nullable;

import com.google.common.collect.ImmutableList;

import mypackage.MyClass;
```

---

## 代码格式

### 大括号

- **K&R 风格**（左大括号不换行）
- 即使是空块也要使用大括号

```java
// 正确
if (condition) {
    doSomething();
} else {
    doSomethingElse();
}

// 错误
if (condition)
{
    doSomething();
}
```

### 块缩进

- 使用 **4 个空格**

### 每行一个语句

```java
// 正确
int a = 1;
int b = 2;

// 错误
int a = 1; int b = 2;
```

### 行长度限制

- 最大 **100** 个字符
- 长行应该合理换行

### 自动换行

```java
// 正确
SomeVeryLongClassName result =
        someVeryLongMethod(
                argument1,
                argument2,
                argument3);
```

### 空格

```java
// 关键字后加空格
if (condition) {
    // ...
}

// 运算符两侧加空格
int result = a + b;

// 逗号后加空格
void method(int a, int b);
```

---

## 命名规范

### 包名

- 全部**小写**
- 使用点分隔

```java
package com.example.myproject;
```

### 类名

- 使用 **PascalCase**（大驼峰命名法）

```java
class MyClass {}
class HttpServer {}
class UrlEncoder {}
```

### 方法名

- 使用 **camelCase**（小驼峰命名法）

```java
void doSomething() {}
int calculateTotal() {}
String getUserName() {}
```

### 常量

- 使用 **UPPER_SNAKE_CASE**

```java
static final int MAX_ITEMS = 100;
static final String DEFAULT_NAME = "unknown";
```

### 非常量字段

- 使用 **camelCase**（小驼峰命名法）

```java
private int itemCount;
protected String userName;
```

### 参数

- 使用 **camelCase**（小驼峰命名法）

```java
void processItem(String itemName, int itemCount) {}
```

### 局部变量

- 使用 **camelCase**（小驼峰命名法）

```java
int totalCount = 0;
String firstName = "John";
```

### 类型变量

- 使用单个大写字母或 PascalCase

```java
class MyType<T> {}
class MyMap<Key, Value> {}
interface Comparable<T> {}
```

---

## 注释

### 块注释

```java
/*
 * 这是块注释
 * 可以跨越多行
 */
```

### 行注释

```java
// 这是行注释
int x = 1;  // 行尾注释
```

### Javadoc

```java
/**
 * 类或接口的描述。
 *
 * <p>更详细的描述。
 *
 * @author 作者名
 * @version 1.0
 */
public class MyClass {

    /**
     * 方法的描述。
     *
     * @param param1 参数1 描述
     * @param param2 参数2 描述
     * @return 返回值描述
     * @throws Exception 异常描述
     */
    public String myMethod(int param1, String param2) throws Exception {
        // ...
    }
}
```

---

## 编程实践

### 使用 @Override

- 重写方法时必须使用 `@Override` 注解

```java
@Override
public String toString() {
    return "MyClass";
}
```

### 捕获异常

- 不要忽略异常
- 使用具体的异常类型

```java
// 正确
try {
    // ...
} catch (IOException e) {
    logger.log(Level.WARNING, "Failed to read file", e);
}

// 错误
try {
    // ...
} catch (Exception e) {
    // 忽略异常
}
```

### 使用静态成员

- 通过类名访问静态成员

```java
// 正确
MyClass.staticMethod();

// 错误
myObject.staticMethod();
```

### 避免 Finalizers

- 不要使用 `finalize()` 方法

### 使用 var

- 可以使用 `var` 进行局部变量类型推断
- 类型应该清晰可见

```java
// 正确
var list = new ArrayList<String>();
var stream = list.stream();

// 避免（类型不清晰）
var result = process();
```

---

## 参考资料

- [Google Java Style Guide (官方)](https://google.github.io/styleguide/javaguide.html)
- [Google 开源项目风格指南（中文）](https://github.com/zh-google-styleguide/zh-google-styleguide)

---

*本文档基于 Google Java Style Guide 整理*
