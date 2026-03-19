---
allowed-tools: Bash(git diff:*), Bash(npm run:*), Bash(npx:*), Bash(python:*), Read, Edit
description: 修复代码评审中发现的问题
---

## Context

- Current git status: !`git status`
- Recent changes: !`git diff HEAD --stat`

## 常见问题修复指南

### 自动可修复
| 类型 | 修复方式 |
|------|----------|
| 代码格式 | `prettier --write` 或 `eslint --fix` |
| 未使用导入 | IDE 自动删除或 `eslint --fix` |
| 简单类型错误 | 添加类型注解 |

### 需手动修复
| 类型 | 处理方式 |
|------|----------|
| 逻辑错误 | 分析并重写逻辑 |
| 安全漏洞 | 使用参数化查询、输入验证等 |
| 性能问题 | 优化算法、添加缓存 |

## Your task

Based on code review feedback:

1. **Analyze the issues** - Understand what needs to be fixed
2. **Auto-fix where possible** - Run linters with --fix flag
3. **Manual fixes** - For complex issues, provide guidance:
   - Show the problematic code
   - Explain the issue
   - Provide corrected code example
4. **Verify fixes** - Run tests or linters to confirm

When making edits:
- Keep changes minimal and focused
- Preserve existing code style
- Add comments if the fix is non-obvious

Report the fixes made and any remaining issues that need manual attention.
