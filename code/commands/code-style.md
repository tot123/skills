---
allowed-tools: Bash(npm run lint:*), Bash(npx eslint:*), Bash(python -m pylint:*), Bash(gofmt:*), Bash(cargo clippy:*), Bash(git diff:*)
description: 代码风格与质量检查
---

## Context

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
