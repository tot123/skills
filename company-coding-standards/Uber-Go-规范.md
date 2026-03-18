# Uber Go 代码规范

> GitHub: https://github.com/uber-go/guide

---

## 目录

- [指导原则](#指导原则)
- [命名规范](#命名规范)
- [注释约定](#注释约定)
- [代码模式](#代码模式)
- [错误处理](#错误处理)
- [并发模式](#并发模式)
- [性能优化](#性能优化)

---

## 指导原则

### 指向接口编程

- 如果接口在包外使用，请使用接口

### 避免全局状态

- 避免使用全局变量
- 使用依赖注入传递状态

### 避免使用 init()

- 尽量避免使用 init() 函数

---

## 命名规范

### 包命名

- 简短、清晰、小写
- 避免使用下划线或驼峰

```go
// good
package json
package http
package sql

// bad
package jsonUtils
package http_client
```

### 函数命名

- 清晰表达意图
- 使用驼峰命名法

```go
// good
func GetUserByID(id int64) (*User, error)
func CalculateTotal(items []Item) int64

// bad
func get_user(id int64) (*User, error)
```

### 接口命名

- 单方法接口使用 -er 后缀

```go
// good
type Reader interface {
    Read(p []byte) (n int, err error)
}

type Writer interface {
    Write(p []byte) (n int, err error)
}
```

### 常量命名

- 使用驼峰命名法

```go
// good
const (
    StatusOK= 200
    StatusNotFound= 404
    maxRetries = 3
)
```

---

## 注释约定

### 包注释

```go
// Package math provides basic constants and mathematical functions.
package math
```

### 函数注释

```go
// Add adds two numbers and returns the result.
func Add(a, b int) int {
    return a + b
}
```

---

## 代码模式

### 结构体初始化

- 使用字段名初始化

```go
// good
user := User{
    ID:1,
    Name: "John",
    Email: "john@example.com",
}

// bad
user := User{1, "John", "john@example.com"}
```

### 使用 defer

```go
// good
func ProcessFile(path string) error {
    f, err := os.Open(path)
    if err != nil {
        return err
    }
    defer f.Close()

    // process file
    return nil
}
```

### 避免嵌套过深

```go
// good
func Process(data []byte) error {
    if len(data) == 0 {
        return errors.New("empty data")
    }

    if !isValid(data) {
        return errors.New("invalid data")
    }

    // process data
    return nil
}
```

---

## 错误处理

### 使用 errors.New

```go
// good
func Divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}
```

### 使用 fmt.Errorf

```go
// good
func ReadConfig(path string) (*Config, error) {
    data, err := os.ReadFile(path)
    if err != nil {
        return nil, fmt.Errorf("failed to read config file %s: %w", path, err)
    }
    // ...
}
```

### 使用 %w 包装错误

```go
// good
if err != nil {
    return fmt.Errorf("context: %w", err)
}
```

---

## 并发模式

### 使用 channel 通信

```go
// good
func ProcessItems(items []Item) []Result {
    results := make(chan Result, len(items))

    for _, item := range items {
        go func(i Item) {
            results <- process(i)
        }(item)
    }

    var allResults []Result
    for range items {
        allResults = append(allResults, <-results)
    }
    return allResults
}
```

### 使用 context

```go
// good
func FetchData(ctx context.Context, url string) ([]byte, error) {
    req, err := http.NewRequestWithContext(ctx, http.MethodGet, url, nil)
    if err != nil {
        return nil, err
    }

    resp, err := http.DefaultClient.Do(req)
    if err != nil {
        return nil, err
    }
    defer resp.Body.Close()

    return io.ReadAll(resp.Body)
}
```

### 使用 sync.WaitGroup

```go
// good
func ProcessConcurrently(items []Item) {
    var wg sync.WaitGroup

    for _, item := range items {
        wg.Add(1)
        go func(i Item) {
            defer wg.Done()
            process(i)
        }(item)
    }

    wg.Wait()
}
```

---

## 性能优化

### 使用 strings.Builder

```go
// bad
func Concat(parts []string) string {
    var result string
    for _, part := range parts {
        result += part
    }
    return result
}

// good
func Concat(parts []string) string {
    var sb strings.Builder
    for _, part := range parts {
        sb.WriteString(part)
    }
    return sb.String()
}
```

### 预分配切片容量

```go
// bad
func Transform(items []Item) []Result {
    var results []Result
    for _, item := range items {
        results = append(results, transform(item))
    }
    return results
}

// good
func Transform(items []Item) []Result {
    results := make([]Result, 0, len(items))
    for _, item := range items {
        results = append(results, transform(item))
    }
    return results
}
```

---

## 参考资料

- [Uber Go Style Guide (GitHub)](https://github.com/uber-go/guide)
- [Uber Go Style Guide 中文版](https://github.com/xxjwxc/uber_go_guide_cn)

---

*本文档基于 Uber Go Style Guide 整理*
