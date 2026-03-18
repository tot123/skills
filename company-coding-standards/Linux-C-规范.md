# Linux 内核 C 代码规范

> 官方文档：https://docs.kernel.org/process/coding-style.html

---

## 目录

- [缩进](#缩进)
- [大括号和空格](#大括号和空格)
- [命名规范](#命名规范)
- [函数](#函数)
- [注释](#注释)
- [代码组织](#代码组织)

---

## 缩进

### 使用 Tab 缩进

- 使用 **Tab** 进行缩进
- 每个 Tab 宽度为 **8 个字符**

```c
/* 正确 */
if (condition) {
        do_something();
}
```

### 行长度

- 每行不超过 **80** 个字符

---

## 大括号和空格

### 大括号风格

- **K&R 风格**：左大括号放在同一行

```c
/* 正确 */
if (condition) {
        action1();
        action2();
} else {
        action3();
}

/* 函数定义是例外 */
int function(int x)
{
        body of function
}
```

### 单行语句

- 即使只有一条语句，也要使用大括号

```c
/* 正确 */
if (condition) {
        do_something();
}
```

### 空格

- 关键字后加空格
- 函数名和括号之间不加空格
- 二元运算符两侧加空格

```c
/* 正确 */
if (x == y) {
        result = a + b * c;
}
```

### 指针声明

- 星号靠近变量名

```c
/* 正确 */
char *p;
int *a, *b;

/* 错误 */
char* p;
int * a, * b;
```

---

## 命名规范

### 全局变量和函数

- 使用**描述性名称**
- 使用**小写字母**和**下划线**

```c
/* 正确 */
int count_active_users(void);
void update_user_status(struct user *u, int status);

/* 错误 */
int CountActiveUsers();
void updateUserStatus(struct user *u, int status);
```

### 局部变量

- 简短、清晰
- 循环变量可以使用 i, j, k

```c
/* 正确 */
int i;
for (i = 0; i < count; i++)
        process(items[i]);
```

### 宏和常量

- 使用**大写字母**和**下划线**

```c
/* 正确 */
#define MAX_USERS 100
#define DEFAULT_TIMEOUT 5000
```

---

## 函数

### 函数长度

- 函数应该**简短**且**专注**
- 理想不超过**1-2 页**

### 函数参数

- 参数数量应该**较少**（通常不超过 5 个）

### 返回值

- 0 表示成功，负数表示错误

```c
/* 正确 */
int do_something(void)
{
        if (error_condition)
                return -EINVAL;

        return 0;  /* 成功 */
}
```

---

## 注释

### 多行注释

```c
/*
 * This is the preferred style for multi-line
 * comments in the Linux kernel source code.
 * Please use it consistently.
 */
```

### 单行注释

```c
/* This is a single-line comment */
```

### 函数注释

```c
/**
 * function_name - Short description
 * @arg1: Description of arg1
 * @arg2: Description of arg2
 *
 * Longer description.
 *
 * Return: Description of return value
 */
int function_name(int arg1, int arg2)
{
        /* ... */
}
```

### 不要使用 C99 风格注释

```c
/* 正确 */
/* This is a comment */

/* 错误 */
// This is a comment
```

---

## 代码组织

### 头文件

```c
#ifndef _MYHEADER_H
#define _MYHEADER_H

#include <linux/types.h>

/* 声明 */

#endif /* _MYHEADER_H */
```

### 源文件结构

```c
/*
 * 文件头注释
 */

#include <linux/module.h>

/* 宏定义 */
#define MAX_ITEMS 100

/* 类型定义 */
struct my_struct {
        int value;
};

/* 函数定义 */
static int helper_function(void)
{
        /* ... */
}

/* 模块初始化 */
static int __init my_module_init(void)
{
        /* ... */
}

/* 模块退出 */
static void __exit my_module_exit(void)
{
        /* ... */
}

module_init(my_module_init);
module_exit(my_module_exit);

MODULE_LICENSE("GPL");
```

---

## 参考资料

- [Linux Kernel Coding Style (官方)](https://docs.kernel.org/process/coding-style.html)
- [Linux 内核代码风格（中文）](https://docs.kernel.org/translations/zh_CN/process/coding-style.html)

---

*本文档基于 Linux Kernel Coding Style 整理*
