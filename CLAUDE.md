# CLAUDE.md

本文件为 Claude Code 提供项目上下文和工作指导。

## 项目概述

这是一个 Claude Code Skills 插件仓库，包含代码提交、评审、风格检查等工具。

## 插件加载方式

### 方式一：启动时指定（临时）

```bash
claude --plugin-dir ./code
```

### 方式二：在 settings.json 中启用（推荐）

编辑 `~/.claude/settings.json`：

```json
{
  "enabledPlugins": {
    "code@local": true
  }
}
```

### 方式三：复制/软链接到插件目录

```bash
# Windows (PowerShell)
Copy-Item -Recurse ./code ~/.claude/plugins/code

# 或软链接
New-Item -ItemType Junction -Path ~/.claude/plugins/code -Target ./code
```

> **注意**：方式一仅当前会话有效；方式二、三为全局启用。

## 可用命令

### Code 插件

| 命令 | 触发条件 | 说明 |
|------|----------|------|
| `/code:push-diff` | 用户需要提交代码 | 查看变更、生成规范提交信息、推送到远端 |
| `/code:style` | 用户需要检查代码风格 | 运行 lint 工具、检查代码规范 |
| `/code:review` | 用户需要进行代码评审 | 分析变更、识别问题、提供改进建议 |
| `/code:review-fix` | 用户需要修复评审问题 | 分析问题、提供修复方案、验证修复 |

## 工作流程

### 1. 提交代码 (`/code:push-diff`)

```
执行步骤：
1. git status 查看变更
2. git diff 分析变更内容
3. 生成符合 Google 规范的提交信息
4. 用户确认后执行 git add/commit/push
```

### 2. 代码风格检查 (`/code:style`)

```
执行步骤：
1. 识别项目语言
2. 检查 lint 配置文件
3. 运行相应工具 (ESLint/Pylint/golint 等)
4. 汇总结果并提供修复建议
```

### 3. 代码评审 (`/code:review`)

```
执行步骤：
1. 获取当前分支变更 (git diff main)
2. 按检查清单评审：
   - 功能正确性
   - 代码质量
   - 安全性
   - 测试覆盖
3. 输出评审报告
```

### 4. 修复评审问题 (`/code:review-fix`)

```
执行步骤：
1. 分析评审意见
2. 自动修复可处理的问题
3. 为复杂问题提供修复指导
4. 运行测试验证
5. 生成修复报告
```

## Google 提交规范速查

### 提交信息模板

```
<类型>: <做什么>

<为什么做这个变更>
<上下文信息>
```

### 首行检查

- [ ] 不超过 50 字符
- [ ] 使用祈使句
- [ ] 描述做什么，而非怎么做
- [ ] 首行后有空行

### 评审检查清单

- [ ] 代码逻辑正确
- [ ] 错误处理完整
- [ ] 无安全漏洞
- [ ] 测试覆盖充分
- [ ] 命名清晰
- [ ] 无重复代码

## 代码规范参考

项目中 `company-coding-standards/` 目录包含各语言的代码规范：

| 语言 | 文件 |
|------|------|
| Python | `Google-Python-规范.md` |
| JavaScript | `Google-JavaScript-规范.md` |
| TypeScript | `Google-TypeScript-规范.md` |
| Go | `Google-Go-规范.md` |
| Java | `Google-Java-规范.md` |
| C++ | `Google-C++-规范.md` |
| Shell | `Google-Shell-规范.md` |

## 注意事项

1. **提交前检查**：确保代码通过 lint 检查
2. **小步提交**：每次提交只做一件事
3. **测试先行**：修复问题后运行相关测试
4. **规范优先**：遵循 Google 工程实践规范
