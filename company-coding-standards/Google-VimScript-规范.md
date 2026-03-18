# Google Vim script 代码规范

> 官方文档：https://google.github.io/styleguide/vimscriptguide.xml

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [编程实践](#编程实践)

---

## 命名规范

### 变量

- 使用 **snake_case**

```vim
" 正确
let user_name = 'John'
let item_count = 10
```

### 函数

- 使用 **PascalCase** 或 **snake_case**

```vim
" 正确
function! MyFunction()
    " ...
endfunction

function! my_function()
    " ...
endfunction
```

### 自定义命令

- 使用 **PascalCase**

```vim
" 正确
command! MyCommand call MyFunction()
```

### 自动命令组

- 使用 **PascalCase**

```vim
" 正确
augroup MyAutoGroup
    autocmd!
    autocmd BufEnter * call OnBufEnter()
augroup END
```

---

## 代码格式

### 缩进

- 使用 **2 个空格**

```vim
" 正确
if condition
  do_something()
endif
```

### 行长度

- 最大 **80** 个字符

### 空格

```vim
" 正确
let x = 1 + 2
call function(arg1, arg2)

" 错误
let x=1+2
call function(arg1,arg2)
```

---

## 编程实践

### 使用 let

```vim
" 正确
let g:my_plugin_enabled = 1
let s:local_variable = 'value'
```

### 使用函数前缀

```vim
" 正确
function! MyPlugin#Init()
    " ...
endfunction

function! MyPlugin#Cleanup()
    " ...
endfunction
```

### 使用自动命令组

```vim
" 正确
augroup MyPlugin
    autocmd!
    autocmd BufEnter * call MyPlugin#OnBufEnter()
    autocmd BufLeave * call MyPlugin#OnBufLeave()
augroup END
```

### 错误处理

```vim
" 正确
try
    call RiskyFunction()
catch
    echoerr 'Error: ' . v:exception
endtry
```

---

## 参考资料

- [Google Vim script Style Guide (官方)](https://google.github.io/styleguide/vimscriptguide.xml)

---

*本文档基于 Google Vim script Style Guide 整理*
