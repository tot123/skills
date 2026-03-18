# Google Shell 代码规范

> 官方文档：https://google.github.io/styleguide/shellguide.html

---

## 目录

- [基本规则](#基本规则)
- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [编程实践](#编程实践)

---

## 基本规则

### 使用 Bash

- 使用 **Bash** 而非其他 shell

```bash
#!/bin/bash
```

### 使用 set

```bash
set -e  # 遇到错误退出
set -u  # 使用未定义变量时报错
set -o pipefail  # 管道中的错误会导致整个管道失败
```

---

## 命名规范

### 变量

- 使用小写字母和下划线
- 常量使用大写

```bash
# 变量
my_variable="value"
user_name="John"

# 常量
readonly MAX_RETRIES=3
readonly DEFAULT_TIMEOUT=30
```

### 函数

- 使用小写字母和下划线

```bash
# 正确
function get_user_name() {
  # ...
}

function calculate_total() {
  # ...
}
```

---

## 代码格式

### 缩进

- 使用 **2 个空格**
- 不要使用 Tab

### 行长度

- 最大 **80** 个字符

### 大括号

- 左大括号与函数名在同一行

```bash
# 正确
function my_function() {
  echo "Hello"
}

# 也正确（省略 function 关键字）
my_function() {
  echo "Hello"
}
```

### 空格

```bash
# 正确
if [[ -f "$file" ]]; then
  echo "File exists"
fi

# 赋值不加空格
my_var="value"
```

---

## 编程实践

### 使用双引号

- 变量使用双引号包裹

```bash
# 正确
echo "$my_var"
if [[ -f "$file_path" ]]; then
  cp "$source" "$destination"
fi

# 错误
echo $my_var
```

### 使用 [[ ]]

- 优先使用 `[[ ]]` 而非 `[ ]`

```bash
# 正确
if [[ "$var" == "value" ]]; then
  # ...
fi

# 不推荐
if [ "$var" = "value" ]; then
  # ...
fi
```

### 使用 $( )

- 优先使用 `$( )` 而非反引号

```bash
# 正确
current_date=$(date)
files=$(ls -la)

# 错误
current_date=`date`
```

### 检查变量

```bash
# 正确
if [[ -z "$my_var" ]]; then
  echo "Variable is empty"
fi

if [[ -n "$my_var" ]]; then
  echo "Variable is not empty"
fi
```

### 使用 local

- 函数内变量使用 local

```bash
# 正确
my_function() {
  local var1="value1"
  local var2="value2"
  # ...
}
```

### 错误处理

```bash
# 正确
if ! cp "$source" "$destination"; then
  echo "Error: Failed to copy file"
  exit 1
fi
```

### 使用 printf

- 优先使用 printf 而非 echo

```bash
# 正确
printf "Hello, %s\n" "$name"

# 避免
echo "Hello, $name"
```

---

## 参考资料

- [Google Shell Style Guide (官方)](https://google.github.io/styleguide/shellguide.html)

---

*本文档基于 Google Shell Style Guide 整理*
