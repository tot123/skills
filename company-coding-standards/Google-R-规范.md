# Google R 代码规范

> 官方文档：https://google.github.io/styleguide/Rguide.html

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [编程实践](#编程实践)

---

## 命名规范

### 变量和函数

- 使用 **snake_case**

```r
# 正确
user_name <- "John"
item_count <- 10
calculate_total <- function() {}
```

### 常量

- 使用 **UPPER_SNAKE_CASE**

```r
# 正确
MAX_ITEMS <- 100
DEFAULT_TIMEOUT <- 30
```

### 类

- 使用 **PascalCase**

```r
# 正确
MyClass <- R6Class("MyClass")
```

---

## 代码格式

### 缩进

- 使用 **2 个空格**

### 赋值

- 使用 `<-` 而非 `=`

```r
# 正确
x <- 1
name <- "John"

# 错误
x = 1
name = "John"
```

### 空格

```r
# 正确
x <- 1 + 2
df[, c("col1", "col2")]
function(arg1, arg2)

# 错误
x<-1+2
df[,c("col1","col2")]
```

### 大括号

```r
# 正确
if (condition) {
    do_something()
} else {
    do_something_else()
}
```

---

## 编程实践

### 使用管道

```r
# 正确
result <- data %>%
    filter(value > 0) %>%
    mutate(new_col = col * 2) %>%
    summarize(total = sum(new_col))
```

### 函数定义

```r
# 正确
calculate_mean <- function(data, na_rm = TRUE) {
    mean(data, na.rm = na_rm)
}
```

### 使用 tidyverse

```r
# 正确
library(dplyr)
library(tidyr)

result <- df %>%
    select(name, value) %>%
    filter(!is.na(value))
```

---

## 参考资料

- [Google R Style Guide (官方)](https://google.github.io/styleguide/Rguide.html)

---

*本文档基于 Google R Style Guide 整理*
