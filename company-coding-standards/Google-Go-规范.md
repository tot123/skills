# Google Go 代码规范

> 官方文档：https://google.github.io/styleguide/go/

---

## 目录

- [代码格式](#代码格式)
- [命名规范](#命名规范)
- [注释](#注释)
- [编程实践](#编程实践)
- [错误处理](#错误处理)

---

## 代码格式

### 使用 gofmt

- 所有代码必须通过 `gofmt` 格式化
- 使用 Tab 缩进

### 行长度

- 没有严格限制
- 但应该保持合理长度

### 括号

- 使用最少的括号

```go
// 正确
if x > 0 {
    // ...
}

// 错误
if (x > 0) {
    // ...
}
```

---

## 命名规范

### 包名

- 全部**小写**
- 简短、有意义
- 不使用下划线或驼峰

```go
package json
package http
package sql
```

### 导出名

- 首字母大写表示导出
- 首字母小写表示私有

```go
// 导出
func MyFunction() {}
const MyConstant = 1
type MyStruct struct {}

// 私有
func myFunction() {}
const myConstant = 1
type myStruct struct {}
```

### 接口命名

- 单方法接口使用 -er 后缀

```go
type Reader interface {
    Read(p []byte) (n int, err error)
}

type Writer interface {
    Write(p []byte) (n int, err error)
}

type Closer interface {
    Close() error
}
```

### 驼峰命名

- 使用 **MixedCaps** 或 **mixedCaps**
- 不使用下划线

```go
// 正确
func writeToFile() {}
type httpRequest struct {}
const maxLength = 100

// 错误
func write_to_file() {}
type HTTPRequest struct {}
const MAX_LENGTH = 100
```

### 缩写

- 保持一致的大小写

```go
// 正确
type URLParser struct {}
func parseURL(url string) {}

// 错误
type UrlParser struct {}
func parseUrl(url string) {}
```

---

## 注释

### 包注释

```go
// Package math provides basic constants and mathematical functions.
//
// This package does not guarantee bit-identical results across program
// executions.
package math
```

### 函数注释

```go
// Add adds two numbers and returns the result.
// It accepts two integers and returns their sum.
func Add(a, b int) int {
    return a + b
}
```

### 类型注释

```go
// Request represents an HTTP request.
type Request struct {
    // Method specifies the HTTP method (GET, POST, etc.)
    Method string

    // URL specifies the URL being requested.
    URL *url.URL
}
```

### 句子风格

- 注释应该是完整的句子
- 以被注释的名称开头

```go
// Request returns the HTTP request.
func Request() *http.Request {}

// Close closes the connection.
func (c *Conn) Close() error {}
```

---

## 编程实践

### 错误处理

- 不要忽略错误

```go
// 正确
file, err := os.Open("file.txt")
if err != nil {
    return nil, err
}

// 错误
file, _ := os.Open("file.txt")
```

### 使用 defer

```go
func ReadFile(path string) ([]byte, error) {
    f, err := os.Open(path)
    if err != nil {
        return nil, err
    }
    defer f.Close()

    return io.ReadAll(f)
}
```

### 避免全局变量

```go
// 正确
type Server struct {
    address string
}

func NewServer(address string) *Server {
    return &Server{address: address}
}

// 错误
var serverAddress string
```

### 使用 context

```go
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

### 避免使用 init()

```go
// 正确
func NewClient() *Client {
    return &Client{
        timeout: 30 * time.Second,
    }
}

// 错误
var defaultClient *Client

func init() {
    defaultClient = &Client{
        timeout: 30 * time.Second,
    }
}
```

---

## 错误处理

### 使用 errors.New

```go
func Divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}
```

### 使用 fmt.Errorf

```go
func ReadConfig(path string) (*Config, error) {
    data, err := os.ReadFile(path)
    if err != nil {
        return nil, fmt.Errorf("failed to read config file %s: %w", path, err)
    }
    // ...
}
```

### 自定义错误类型

```go
type ValidationError struct {
    Field   string
    Message string
}

func (e *ValidationError) Error() string {
    return fmt.Sprintf("validation error on %s: %s", e.Field, e.Message)
}
```

---

## 参考资料

- [Google Go Style Guide (官方)](https://google.github.io/styleguide/go/)
- [Effective Go](https://golang.org/doc/effective_go)
- [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)

---

*本文档基于 Google Go Style Guide 整理*
