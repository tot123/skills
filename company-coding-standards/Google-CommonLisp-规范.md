# Google Common Lisp 代码规范

> 官方文档：https://google.github.io/styleguide/lispguide.html

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [编程实践](#编程实践)

---

## 命名规范

### 变量和函数

- 使用 **kebab-case**（连字符分隔）

```lisp
;; 正确
(defun calculate-total (items)
  ...)

(defparameter *max-items* 100)
```

### 全局变量

- 使用 **\*earmuffs\***（星号包围）

```lisp
;; 正确
(defparameter *default-timeout* 30)
(defvar *user-database* nil)
```

### 常量

- 使用 **+plus-signs+**

```lisp
;; 正确
(defconstant +max-retries+ 3)
(defconstant +default-port+ 8080)
```

### 类和结构体

- 使用 **\<angle-brackets\>** 或 PascalCase

```lisp
;; 正确
(defclass <user> ()
  ((name :accessor user-name
         :initarg :name)
   (age :accessor user-age
        :initarg :age)))
```

---

## 代码格式

### 缩进

- 使用 **2 个空格**

```lisp
;; 正确
(defun my-function (arg1 arg2)
  (let ((x 1)
        (y 2))
    (+ x y)))
```

### 括号风格

- 右括号不单独成行

```lisp
;; 正确
(defun foo ()
  (if condition
      (do-something)
      (do-something-else)))

;; 错误
(defun foo ()
  (if condition
      (do-something)
      (do-something-else)
   )
 )
```

### 空格

```lisp
;; 正确
(let ((x 1)
      (y 2))
  (+ x y))

;; 错误
(let((x 1)(y 2))
  (+x y))
```

---

## 编程实践

### 使用 let 和 let*

```lisp
;; 正确
(let ((x 1)
      (y 2))
  (+ x y))

(let* ((x 1)
       (y (+ x 1)))
  (+ x y))
```

### 使用 defun

```lisp
;; 正确
(defun calculate-total (items)
  (reduce #'+ items :key #'item-price))
```

### 使用宏

```lisp
;; 正确
(defmacro with-file ((var filename) &body body)
  `(with-open-file (,var ,filename)
     ,@body))
```

### 条件语句

```lisp
;; 正确
(if condition
    (then-clause)
    (else-clause))

(cond
  ((= x 1) 'one)
  ((= x 2) 'two)
  (t 'other))
```

---

## 参考资料

- [Google Common Lisp Style Guide (官方)](https://google.github.io/styleguide/lispguide.html)

---

*本文档基于 Google Common Lisp Style Guide 整理*
