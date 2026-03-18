# Google Markdown 代码规范

> 官方文档：https://google.github.io/styleguide/docguide/style.html

---

## 目录

- [基本规则](#基本规则)
- [文档结构](#文档结构)
- [格式规范](#格式规范)
- [最佳实践](#最佳实践)

---

## 基本规则

### 文件扩展名

- 使用 `.md` 扩展名

### 换行

- 每行不超过 **80** 个字符
- 句子之间使用一个换行

---

## 文档结构

### 标题

```markdown
# 一级标题

## 二级标题

### 三级标题
```

### 目录

- 长文档应包含目录

```markdown
## 目录

- [标题1](#标题1)
- [标题2](#标题2)
```

---

## 格式规范

### 空行

- 标题前后各一个空行
- 列表前后各一个空行

```markdown
## 标题

段落内容。

- 列表项1
- 列表项2

段落内容。
```

### 列表

```markdown
- 无序列表项1
- 无序列表项2

1. 有序列表项1
2. 有序列表项2
```

### 代码块

```markdown
行内代码：`code`

代码块：

\`\`\`language
code here
\`\`\`
```

### 链接

```markdown
[链接文本](https://example.com)

[带标题的链接](https://example.com "链接标题")
```

### 图片

```markdown
![图片描述](image.png)

![带标题的图片](image.png "图片标题")
```

### 强调

```markdown
*斜体*
**粗体**
```

---

## 最佳实践

### 使用清晰的标题

```markdown
# 项目名称

简短描述

## 安装

安装说明

## 使用方法

使用说明

## API 文档

API 说明
```

### 链接引用

```markdown
[Google][google] 是一个搜索引擎。

[google]: https://google.com
```

### 表格

```markdown
| 列1 | 列2 | 列3 |
|-----|-----|-----|
| 值1 | 值2 | 值3 |
| 值4 | 值5 | 值6 |
```

---

## 参考资料

- [Google Markdown Style Guide (官方)](https://google.github.io/styleguide/docguide/style.html)

---

*本文档基于 Google Markdown Style Guide 整理*
