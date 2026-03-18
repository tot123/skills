# Google Swift 代码规范

> 官方文档：https://google.github.io/styleguide/swift.html

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [编程实践](#编程实践)

---

## 命名规范

### 类和结构体

- 使用 **PascalCase**

```swift
// 正确
class HttpClient {}
struct UserProfile {}
enum HttpStatus {}
```

### 函数和方法

- 使用 **camelCase**

```swift
// 正确
func calculateTotal() -> Int {}
func getUserById(_ id: Int) -> User? {}
```

### 变量和常量

- 使用 **camelCase**

```swift
// 正确
var userName = "John"
let maxRetryCount = 3
```

### 枚举值

- 使用 **camelCase**

```swift
// 正确
enum HttpStatus {
    case ok
    case notFound
    case internalServerError
}
```

### 协议

- 使用 **PascalCase**
- 描述能力的协议以 -ing, -able, -ible 结尾

```swift
// 正确
protocol Codable {}
protocol Comparable {}
protocol Loading {}
```

---

## 代码格式

### 缩进

- 使用 **2 个空格**

### 大括号

- 左大括号放在同一行

```swift
// 正确
if condition {
    doSomething()
} else {
    doSomethingElse()
}
```

### 空格

```swift
// 正确
let x = 1 + 2
func foo(a: Int, b: Int) {}
```

### 分号

- 不使用分号

```swift
// 正确
let x = 1
doSomething()

// 错误
let x = 1;
doSomething();
```

---

## 编程实践

### 使用 guard 和 if let

```swift
// 正确
guard let user = user else {
    return
}

if let name = user.name {
    print(name)
}
```

### 使用可选链

```swift
// 正确
let name = user?.profile?.name
```

### 使用 nil 合并

```swift
// 正确
let name = userName ?? "Unknown"
```

### 使用 defer

```swift
// 正确
func processFile() {
    let file = openFile()
    defer {
        closeFile(file)
    }
    // process file
}
```

### 使用 extension 组织代码

```swift
// 正确
class MyClass {
    // 核心属性和方法
}

extension MyClass {
    // 辅助方法
}

extension MyClass: Codable {
    // 协议实现
}
```

---

## 参考资料

- [Google Swift Style Guide (官方)](https://google.github.io/styleguide/swift.html)

---

*本文档基于 Google Swift Style Guide 整理*
