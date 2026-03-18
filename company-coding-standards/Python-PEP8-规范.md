# Python PEP 8 代码规范

> 官方文档：https://peps.python.org/pep-0008/

---

## 目录

- [简介](#简介)
- [代码布局](#代码布局)
- [命名约定](#命名约定)
- [编程建议](#编程建议)

---

## 简介

PEP 8 是 Python 官方的代码风格指南，旨在提高代码可读性。

**重要原则**：
- 一致性很重要
- 项目内部一致性比遵循本指南更重要
- 知道什么时候不需要保持一致

---

## 代码布局

### 缩进

- 使用 **4 个空格**

```python
# 正确
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)
```

### Tab 还是空格

- **空格是首选**
- Tab 只用于与已有代码保持一致

### 行长度

- 最大 **79** 个字符
- 文档字符串/注释：**72** 个字符

### 空行

- 顶层函数和类：**2 个空行**
- 类内方法：**1 个空行**

### 导入

```python
# 正确
import os
import sys

from subprocess import Popen, PIPE
```

**导入顺序**：
1. 标准库
2. 第三方库
3. 本地库

---

## 命名约定

### 命名风格

| 风格 | 示例 | 用途 |
|------|------|------|
| 小写 | `lowercase` | 变量、函数 |
| 下划线小写 | `lower_case_with_underscores` | 变量、函数 |
| 大写 | `UPPERCASE` | 常量 |
| 下划线大写 | `UPPER_CASE_WITH_UNDERSCORES` | 常量 |
| 驼峰 | `CapitalizedWords` | 类 |

### 类命名

- 使用 **PascalCase**

```python
class MyClass:
    pass

class HttpServer:
    pass
```

### 函数和变量命名

- 使用 **snake_case**

```python
def my_function():
    pass

my_variable = 1
```

### 常量

- 使用 **UPPER_SNAKE_CASE**

```python
MAX_OVERFLOW = 100
TOTAL = 0
```

### 私有变量

- 单下划线前缀表示内部使用
- 双下划线前缀触发名称修饰

```python
_internal_variable = 1
__private_variable = 2
```

---

## 编程建议

### 与 None 比较

```python
# 正确
if foo is not None:

# 错误
if not foo is None:
```

### 使用 def 而非 lambda 赋值

```python
# 正确
def f(x): return 2 * x

# 错误
f = lambda x: 2 * x
```

### 异常处理

```python
# 正确
try:
    value = collection[key]
except KeyError:
    return key_not_found(key)
```

### 使用 startswith/endswith

```python
# 正确
if foo.startswith('bar'):

# 错误
if foo[:3] == 'bar':
```

### 使用 isinstance

```python
# 正确
if isinstance(obj, int):

# 错误
if type(obj) is type(1):
```

### 检查空序列

```python
# 正确
if not seq:
if seq:

# 错误
if len(seq):
if not len(seq):
```

### 布尔值比较

```python
# 错误
if greeting == True:

# 更错误
if greeting is True:
```

### 类型注解

```python
# 正确
def munge(input: AnyStr) -> PosInt:
    ...

code: int

class Point:
    coords: Tuple[int, int]
    label: str = '<unknown>'
```

---

## 参考资料

- [PEP 8 官方文档](https://peps.python.org/pep-0008/)
- [PEP 257 - Docstring Conventions](https://peps.python.org/pep-0257/)

---

*本文档基于 PEP 8 整理*
