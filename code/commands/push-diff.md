---
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*)
description: 提交代码到远端代码库，遵循 Google 提交规范
user-provided: |
  仅当用户明确表达以下意图时才触发此命令：
  - "帮我提交代码"、"commit"、"push"
  - "运行 /code:push-diff"
  - "使用 push-diff 命令"

  不要在以下情况自动触发：
  - 用户只是询问代码问题
  - 用户在做其他任务（如代码评审、风格检查）
  - 用户没有明确要求提交
---

## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD --stat`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -5`

## Google 提交规范

### 首行格式
- 简短摘要，描述做了什么（不超过 50 字符）
- 使用祈使句（如 "Add feature" 而非 "Adding feature"）
- 首行后空一行

### 类型前缀
- feat: 新功能
- fix: Bug 修复
- refactor: 重构
- docs: 文档更新
- style: 代码格式
- test: 测试相关
- chore: 构建/工具
- perf: 性能优化

### 好的示例
```
feat: Add user authentication module

Implement JWT-based authentication with refresh token support.
This enables secure API access and session management.
```

### 不好的示例
```
Fix bug
Add patch
Phase 1
```

## Your task

Based on the above changes, create a git commit following Google commit message conventions.

1. Analyze the changes and generate a proper commit message
2. Stage the relevant files with `git add`
3. Create the commit with the generated message
4. Push to the remote repository

Do not use any other tools or do anything else.
