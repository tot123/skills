# Google C# 代码规范

> 官方文档：https://google.github.io/styleguide/csharp-style.html

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [编程实践](#编程实践)

---

## 命名规范

### 类和命名空间

- 使用 **PascalCase**

```csharp
// 正确
public class HttpClient {}
namespace MyApplication.Services {}
```

### 方法

- 使用 **PascalCase**

```csharp
// 正确
public void CalculateTotal() {}
public string GetUserName() {}
```

### 属性

- 使用 **PascalCase**

```csharp
// 正确
public string UserName { get; set; }
public int ItemCount { get; private set; }
```

### 变量

- 局部变量：**camelCase**
- 私有字段：**_camelCase**（下划线前缀）

```csharp
// 正确
public class MyClass
{
    private int _itemCount;
    private readonly string _userName;

    public void Process()
    {
        int totalCount = 0;
        string firstName = "John";
    }
}
```

### 常量

- 使用 **PascalCase**

```csharp
// 正确
public const int MaxItems = 100;
public const string DefaultName = "unknown";
```

### 接口

- 使用 **I** 前缀 + PascalCase

```csharp
// 正确
public interface IUserService {}
public interface IRepository<T> {}
```

### 事件

- 使用 **PascalCase**
- 使用动词或动词短语

```csharp
// 正确
public event EventHandler Click;
public event EventHandler DataLoaded;
```

---

## 代码格式

### 缩进

- 使用 **4 个空格**

### 大括号

- 左大括号放在同一行（Allman 风格也允许）

```csharp
// 正确
if (condition)
{
    DoSomething();
}
else
{
    DoSomethingElse();
}
```

### 空格

```csharp
// 正确
if (x == y)
{
    result = a + b * c;
}

// 方法调用
var result = CalculateTotal(a, b);
```

### using 语句

- 放在文件顶部
- 按字母顺序排序

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using MyApplication.Services;
```

---

## 编程实践

### 使用 var

- 类型明显时可以使用 var

```csharp
// 正确
var list = new List<string>();
var count = items.Count();

// 避免（类型不明显）
var result = ProcessData();
```

### 使用表达式体成员

```csharp
// 正确
public string FullName => $"{FirstName} {LastName}";
public override string ToString() => $"{Name} ({Id})";
```

### 使用字符串插值

```csharp
// 正确
var message = $"Hello, {userName}!";

// 错误
var message = string.Format("Hello, {0}!", userName);
```

### 使用 null 条件运算符

```csharp
// 正确
var name = user?.Profile?.Name;
user?.Save();
```

### 使用 async/await

```csharp
// 正确
public async Task<User> GetUserAsync(int id)
{
    var user = await _repository.FindAsync(id);
    return user;
}
```

---

## 参考资料

- [Google C# Style Guide (官方)](https://google.github.io/styleguide/csharp-style.html)

---

*本文档基于 Google C# Style Guide 整理*
