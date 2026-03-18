---
description: 提交代码到远端代码库
tags: [git, commit, push]
---

# push-diff

提交代码到远端代码库，遵循 Google 提交规范。

## 功能

1. **查看变更差异** - 显示待提交的代码变更
2. **生成规范提交信息** - 按照 Google CL 描述规范生成提交信息
3. **推送到远程仓库** - 将代码推送到远端

## Google 提交信息规范

### 首行格式

- 简短摘要，描述做了什么
- 使用祈使句（如 "Add feature" 而非 "Adding feature"）
- 不超过 50 字符
- 首行后空一行

### 正文格式

- 解释**为什么**做这个变更
- 提供上下文信息（bug 号、设计文档链接等）
- 说明方案的优缺点

### 类型前缀（推荐）

```
feat:     新功能
fix:      Bug 修复
refactor: 重构
docs:     文档更新
style:    代码格式（不影响逻辑）
test:     测试相关
chore:    构建/工具相关
perf:     性能优化
```

### 示例

**好的提交信息：**

```
RPC: Remove size limit on RPC server message freelist.

Servers like FizzBuzz have very large messages and would benefit from reuse.
Make the freelist larger, and add a goroutine that frees the freelist entries
slowly over time, so that idle servers eventually release all freelist entries.
```

**不好的提交信息：**

```
Fix bug
Fix build
Add patch
Moving code from A to B
Phase 1
```

## 执行步骤

当用户调用此命令时：

1. 运行 `git status` 查看变更状态
2. 运行 `git diff` 查看具体变更
3. 分析变更内容，生成符合规范的提交信息
4. 询问用户确认提交信息
5. 执行 `git add` 和 `git commit`
6. 执行 `git push` 推送到远端

## 参考资源

- [Google Engineering Practices - CL Descriptions](https://google.github.io/eng-practices/review/developer/cl-descriptions.html)
- [Conventional Commits](https://www.conventionalcommits.org/)
