---
description: 代码提交与评审工具集，遵循 Google 工程实践规范
commands:
  - name: push-diff
    description: 提交代码到远端代码库
  - name: code-style
    description: 代码风格与质量检查
  - name: code-review
    description: 代码评审
  - name: code-review-fix
    description: 修复代码评审问题
---

# code

代码提交与评审工具集，提供代码推送、风格检查、代码评审等功能。

## 命令列表

| 命令 | 说明 |
|------|------|
| `/code:push-diff` | 提交代码到远端代码库 |
| `/code:code-style` | 代码风格与质量检查 |
| `/code:code-review` | 代码评审 |
| `/code:code-review-fix` | 修复代码评审问题 |

## 使用方式

```
/code:push-diff       # 提交代码变更
/code:code-style      # 检查代码风格
/code:code-review     # 进行代码评审
/code:code-review-fix # 修复评审问题
```

## Google 提交规范参考

本插件遵循 Google 工程实践规范，详见各子命令文档。
