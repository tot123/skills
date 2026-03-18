# Google C++ 代码规范

> 官方文档：https://google.github.io/styleguide/cppguide.html

---

## 目录

- [头文件](#头文件)
- [作用域](#作用域)
- [命名规范](#命名规范)
- [注释](#注释)
- [格式](#格式)
- [其他规则](#其他规则)

---

## 头文件

### #define 保护

所有头文件都应该使用 `#define` 防止多重包含，命名格式为：

```cpp
#ifndef PROJECT_PATH_FILE_H_
#define PROJECT_PATH_FILE_H_

// 头文件内容

#endif  // PROJECT_PATH_FILE_H_
```

### 前置声明

- 尽可能避免使用前置声明
- 优先使用 `#include`

### 内联函数

- 只有当函数体很小（10行或更少）时才定义为内联函数
- 析构函数通常不应该是内联的

### 函数参数顺序

参数顺序：输入参数在前，输出参数在后。

```cpp
// 正确
void Foo(int input, std::string* output);
```

---

## 作用域

### 命名空间

- 在 `.cc` 文件中使用匿名命名空间或 static 声明
- 不要在头文件中使用匿名命名空间
- 不要使用 using 指令引入整个命名空间

```cpp
// 正确
namespace myproject {
namespace internal {

void Foo() {
    // ...
}

}  // namespace internal
}  // namespace myproject
```

### 嵌套类

- 嵌套类可以在被使用的地方定义为前置声明
- 不要将嵌套类定义为 public，除非它们是接口的一部分

### 静态成员

- 优先使用静态成员函数或命名空间内的函数
- 避免使用静态全局变量

---

## 命名规范

### 通用规则

- 使用描述性名称
- 不要使用缩写，除非是广泛认可的
- 避免使用类似数字的字符

### 类型命名

- 使用 **PascalCase**（大驼峰命名法）

```cpp
// 类和结构体
class UrlTable { ... };
class UrlTableTester { ... };
struct UrlTableProperties { ... };

// 类型定义
typedef hash_map<UrlTableProperties *, std::string> PropertiesMap;

// using 别名
using PropertiesMap = hash_map<UrlTableProperties *, std::string>;
```

### 变量命名

- **普通变量**：snake_case（小写+下划线）
- **类成员变量**：snake_case_（末尾加下划线）
- **结构体成员变量**：snake_case（不加下划线）
- **常量**：kCamelCase（k 开头+驼峰）

```cpp
// 普通变量
std::string table_name;

// 类成员变量
class TableInfo {
  private:
    std::string table_name_;  // 末尾下划线
    static int instance_count_;
};

// 结构体成员变量
struct UrlTableProperties {
    std::string name;
    int num_entries;
};

// 常量
const int kDaysInAWeek = 7;
```

### 函数命名

- **普通函数**：PascalCase（大驼峰命名法）
- **存取函数**：与变量名相同

```cpp
// 普通函数
void AddTableEntry();
bool DeleteUrl(const std::string& url);

// 存取函数
class MyClass {
  public:
    int num_entries() const { return num_entries_; }
    void set_num_entries(int num) { num_entries_ = num; }
  private:
    int num_entries_;
};
```

### 命名空间命名

- 使用 **snake_case**（小写+下划线）

```cpp
namespace http_server {
    // ...
}
```

### 枚举命名

- 使用 **kCamelCase**（k 开头+驼峰）

```cpp
enum UrlTableErrors {
    kOK = 0,
    kErrorOutOfMemory,
    kErrorMalformedInput,
};
```

### 宏命名

- 使用 **UPPER_SNAKE_CASE**（大写+下划线）

```cpp
#define PI_ROUNDED 3.0
#define ROUND(x) ...
```

---

## 注释

### 注释风格

- 使用 `//` 或 `/* */`
- `//` 更常用

### 文件注释

```cpp
// Copyright 2024 Google Inc. All Rights Reserved.
//
// Licensed under the Apache License, Version 2.0 (the "License");
// ...
```

### 类注释

```cpp
// Iterates over the contents of a GargantuanTable.
// Example:
//    GargantuanTableIterator* iter = table->NewIterator();
//    for (iter->Seek("foo"); !iter->done(); iter->Next()) {
//      process(iter->key(), iter->value());
//    }
//    delete iter;
class GargantuanTableIterator {
    // ...
};
```

### 函数注释

```cpp
// Returns an iterator for this table.  It is the client's
// responsibility to delete the iterator when it is done with it,
// and it must not use the iterator once the GargantuanTable object
// on which the iterator was created has been deleted.
//
// The iterator is initially positioned at the beginning of the table.
//
// This method is equivalent to:
//    std::unique_ptr<Iterator> iter = table->NewIterator();
//    iter->Seek("");
//    return iter;
std::unique_ptr<Iterator> NewIterator() const;
```

### 变量注释

```cpp
int num_errors;        // Number of errors encountered during processing.
int num_completed_connections;  // Number of connections that have completed.
```

---

## 格式

### 行长度

- 每行最多 **80** 个字符

### 缩进

- 使用 **2 个空格** 缩进
- 不要使用 Tab

### 大括号

- **K&R 风格**：左大括号放在同一行

```cpp
// 条件语句
if (condition) {
    // ...
} else {
    // ...
}

// 循环
for (int i = 0; i < 10; ++i) {
    // ...
}

// 函数
void Foo() {
    // ...
}
```

### 空格

```cpp
// 运算符两侧加空格
x = 0;
v = w * x + y / z;
v = w * (x + z);

// 逗号后加空格
void Foo(int x, int y);

// 冒号后加空格
class MyClass : public BaseClass {
    // ...
};

// 指针和引用
char *c;
const std::string &str;
```

### 空行

- 在逻辑块之间使用空行
- 不要有过多的空行

---

## 其他规则

### 智能指针

- 优先使用 `std::unique_ptr`
- 使用 `std::shared_ptr` 当需要共享所有权时
- 不要使用 `std::auto_ptr`

### RTTI

- 避免使用运行时类型信息（RTTI）
- 使用虚函数、模板或重载代替

### 类型转换

- 使用 C++ 风格的类型转换
- 不要使用 C 风格的类型转换

```cpp
// 正确
int64_t value = static_cast<int64_t>(double_value);
const_cast<MyClass*>(ptr);

// 错误
int64_t value = (int64_t)double_value;
```

### 异常

- 不使用 C++ 异常
- 使用错误码或其他机制

### 流

- 只在日志中使用流
- 其他情况使用 `printf` 或类似函数

---

## 参考资料

- [Google C++ Style Guide (官方)](https://google.github.io/styleguide/cppguide.html)
- [Google 开源项目风格指南（中文）](https://github.com/zh-google-styleguide/zh-google-styleguide)

---

*本文档基于 Google C++ Style Guide 整理*
