---
allowed-tools: Bash(git diff:*), Bash(git log:*), Bash(git branch:*)
description: 代码评审，检查代码质量、安全性和最佳实践
user-provided: |
  仅当用户明确表达以下意图时才触发此命令：
  - "代码评审"、"review"、"review this code"
  - "运行 /code:review"
  - "使用 review 命令"

  不要在以下情况自动触发：
  - 用户只是询问代码问题
  - 用户在做其他任务（如提交代码、风格检查）
  - 用户没有明确要求代码评审
---

## 可用工具

| 工具 | 用途 | 使用场景 |
|------|------|----------|
| `Bash(git diff:*)` | 查看代码变更 | 对比当前分支与主分支的差异 |
| `Bash(git log:*)` | 查看提交历史 | 了解最近的代码变更记录 |
| `Bash(git branch:*)` | 查看分支信息 | 确认当前工作分支 |

## Context

- Language: !`grep -i "^language:" CLAUDE.md 2>/dev/null | head -1 | cut -d: -f2 | tr -d ' ' || echo "zh-CN"`
- Current branch: !`git branch --show-current`
- Changes compared to main: !`git diff main...HEAD --stat 2>/dev/null || git diff origin/main...HEAD --stat 2>/dev/null || echo "Cannot compare to main"`
- Recent commits: !`git log --oneline -10`
- Full diff: !`git diff main...HEAD 2>/dev/null || git diff origin/main...HEAD 2>/dev/null || git diff HEAD~1..HEAD`

## Code Review Checklist

### 功能正确性
- [ ] 代码是否实现了预期功能？
- [ ] 边界条件是否处理正确？
- [ ] 错误处理是否完整？

### 代码质量
- [ ] 命名是否清晰、有意义？
- [ ] 是否有重复代码可以抽取？
- [ ] 函数/方法是否过长需要拆分？
- [ ] 注释是否充分且有意义？

### 安全性
- [ ] 是否有 SQL 注入风险？
- [ ] 是否有 XSS 漏洞？
- [ ] 敏感数据是否正确处理？
- [ ] 输入验证是否充分？

### 性能
- [ ] 是否有明显的性能问题？
- [ ] 数据库查询是否高效？
- [ ] 是否有不必要的循环或计算？

### 测试
- [ ] 新代码是否有测试覆盖？
- [ ] 边界情况是否被测试？

## Your task

Review the code changes and provide:
1. Summary of changes
2. Issues found (categorized by severity: Critical/Major/Minor)
3. Suggestions for improvement
4. Overall assessment

Be constructive and specific in your feedback.
