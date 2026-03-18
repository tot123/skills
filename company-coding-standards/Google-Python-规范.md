# Google Python 代码规范

> 官方文档：https://google.github.io/styleguide/pyguide.html

---

## 目录

- [Python 版本](#python-版本)
- [代码格式](#代码格式)
- [命名规范](#命名规范)
- [注释](#注释)
- [类型注解](#类型注解)
- [编程实践](#编程实践)

---

## Python 版本

- 使用 **Python 3** (3.6+)
- 代码应该兼容 Python 3

---

## 代码格式

### 行长度

- 最大行长度：**80** 个字符
- 长行可以使用括号隐式续行

### 缩进

- 使用 **4 个空格**
- 不要使用 Tab

### 空行

- 顶层函数和类定义之间：**2 个空行**
- 类方法之间：**1 个空行**

### 导入

```python
# 标准库
import os
import sys

# 第三方库
import numpy as np
import tensorflow as tf

# 本地库
from myproject import mymodule
```

### 字符串

- 优先使用 **三引号** 字符串（`"""`）
- 使用 `f-string` 进行字符串格式化

```python
# 正确
name = f"Hello, {user_name}"

# 避免
name = "Hello, %s" % user_name
name = "Hello, {}".format(user_name)
```

---

## 命名规范

### 模块和包

- 模块：**snake_case**
- 包：**snake_case**

```python
# 模块名
my_module.py

# 包名
my_package/
```

### 类

- 使用 **PascalCase**（大驼峰命名法）

```python
class MyClass:
    pass

class HttpServer:
    pass
```

### 函数和方法

- 使用 **snake_case**
- 私有方法：前缀下划线

```python
def my_function():
    pass

def _private_method(self):
    pass
```

### 变量

- 使用 **snake_case**
- 私有变量：前缀下划线
- 保护变量：前缀双下划线

```python
my_variable = 1
_private_variable = 2
__protected_variable = 3
```

### 常量

- 使用 **UPPER_SNAKE_CASE**

```python
MAX_OVERFLOW = 100
DEFAULT_TIMEOUT = 30
```

---

## 注释

### 模块注释

```python
"""模块的一句话概述。

更详细的模块描述。
"""
```

### 函数注释

```python
def fetch_rows(table: str, keys: List[str]) -> Dict[str, Any]:
    """从表中获取行数据。

    Args:
        table: 表名
        keys: 要获取的键列表

    Returns:
        键到行数据的映射字典

    Raises:
        IOError: 如果无法读取表
    """
    pass
```

### 类注释

```python
class MyServer:
    """服务器类的一句话概述。

    更详细的类描述。

    Attributes:
        host: 服务器主机名
        port: 服务器端口号
    """
```

---

## 类型注解

### 基本类型

```python
def add(a: int, b: int) -> int:
    return a + b

def greet(name: str) -> str:
    return f"Hello, {name}"
```

### 容器类型

```python
from typing import List, Dict, Set, Tuple

def process_items(items: List[str]) -> Dict[str, int]:
    pass

def get_coordinates() -> Tuple[float, float]:
    pass
```

### 可选类型

```python
from typing import Optional

def find_user(user_id: int) -> Optional[User]:
    pass
```

### 联合类型

```python
from typing import Union

def process(value: Union[int, str]) -> None:
    pass
```

### Any 类型

```python
from typing import Any

def process_any(value: Any) -> None:
    pass
```

---

## 编程实践

### 变量声明

- 变量名应该描述其用途
- 避免使用单字母变量名（循环变量除外）

```python
# 正确
for user in users:
    process(user)

# 避免
for u in users:
    process(u)
```

### 默认参数

- 不要使用可变对象作为默认参数

```python
# 错误
def append_to(element, to_list=[]):
    to_list.append(element)
    return to_list

# 正确
def append_to(element, to_list=None):
    if to_list is None:
        to_list = []
    to_list.append(element)
    return to_list
```

### 属性

- 使用 `@property` 装饰器实现简单的计算属性

```python
class Circle:
    def __init__(self, radius: float):
        self.radius = radius

    @property
    def area(self) -> float:
        return 3.14159 * self.radius ** 2
```

### True/False 求值

```python
# 正确
if my_list:
    pass

if not my_dict:
    pass

# 避免
if len(my_list) > 0:
    pass

if my_dict == {}:
    pass
```

### 异常处理

```python
# 正确
try:
    value = my_dict[key]
except KeyError:
    return default_value

# 避免
try:
    value = my_dict[key]
except:
    return default_value
```

---

## 参考资料

- [Google Python Style Guide (官方)](https://google.github.io/styleguide/pyguide.html)
- [Google 开源项目风格指南（中文）](https://github.com/zh-google-styleguide/zh-google-styleguide)

---

*本文档基于 Google Python Style Guide 整理*
