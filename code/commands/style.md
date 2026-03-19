---
allowed-tools: Bash(npm run lint:*), Bash(npx eslint:*), Bash(python -m pylint:*), Bash(gofmt:*), Bash(cargo clippy:*), Bash(git diff:*)
description: 代码风格与质量检查
---

## 可用工具

| 工具 | 用途 | 使用场景 |
|------|------|----------|
| `Bash(npm run lint:*)` | 运行 npm lint 脚本 | 执行项目配置的 lint 检查 |
| `Bash(npx eslint:*)` | 执行 ESLint | JavaScript/TypeScript 代码规范检查 |
| `Bash(python -m pylint:*)` | 执行 Pylint | Python 代码规范检查 |
| `Bash(gofmt:*)` | 格式化 Go 代码 | Go 代码格式化检查 |
| `Bash(cargo clippy:*)` | 执行 Clippy | Rust 代码质量检查 |
| `Bash(git diff:*)` | 查看代码变更 | 分析待检查的文件范围 |

## Context

- Language: !`grep -i "^language:" CLAUDE.md 2>/dev/null | head -1 | cut -d: -f2 | tr -d ' ' || echo "zh-CN"`
- Current directory files: !`ls -la`
- Package.json scripts (if exists): !`cat package.json 2>/dev/null | grep -A 20 '"scripts"' || echo "No package.json"`
- Python requirements (if exists): !`ls *.txt *.cfg pyproject.toml 2>/dev/null || echo "No Python project files"`
- Current git changes: !`git diff --stat HEAD 2>/dev/null || echo "No changes"`

## Your task

Analyze the project and run appropriate lint/style check tools:

1. **Identify the project type:**
   - JavaScript/TypeScript: ESLint, Prettier
   - Python: Pylint, Black, Flake8
   - Go: gofmt, golint
   - Rust: cargo clippy
   - Java: Checkstyle, Spotless

2. **Run the appropriate linter:**
   - Check if lint scripts exist in package.json
   - Run the configured lint command
   - If no lint config, suggest setting one up

3. **Report findings:**
   - List any style violations
   - Suggest fixes for common issues
   - Provide auto-fix commands if available

Focus on code quality, consistency, and best practices.
