# Claude 如何记忆你的项目

> 使用 CLAUDE.md 文件给 Claude 持久指令，并让 Claude 通过自动记忆自动积累学习。

每个 Claude Code 会话都以一个新的上下文窗口开始。两种机制跨会话传递知识：

* **CLAUDE.md 文件**：你编写的指令，给 Claude 持久上下文
* **自动记忆**：Claude 根据你的更正和偏好自己写的笔记

## CLAUDE.md vs 自动记忆

| | CLAUDE.md 文件 | 自动记忆 |
|---|---|---|
| **谁写的** | 你 | Claude |
| **包含什么** | 指令和规则 | 学习和模式 |
| **范围** | 项目、用户或组织 | 每个工作树 |
| **加载到** | 每个会话 | 每个会话（前 200 行） |
| **用于** | 编码标准、工作流程、项目架构 | 构建命令、调试见解、Claude 发现的偏好 |

## CLAUDE.md 文件

CLAUDE.md 文件是为项目、个人工作流程或整个组织提供持久指令的 markdown 文件。

### CLAUDE.md 文件存放位置

| 范围 | 位置 | 用途 | 共享给 |
|------|------|------|--------|
| **托管策略** | macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`<br>Linux/WSL: `/etc/claude-code/CLAUDE.md`<br>Windows: `C:\Program Files\ClaudeCode\CLAUDE.md` | IT/DevOps 管理的组织范围指令 | 组织中的所有用户 |
| **项目指令** | `./CLAUDE.md` 或 `./.claude/CLAUDE.md` | 项目的团队共享指令 | 通过版本控制的团队成员 |
| **用户指令** | `~/.claude/CLAUDE.md` | 所有项目的个人偏好 | 只有你（所有项目） |
| **本地指令** | `./CLAUDE.local.md` | 不提交到 git 的个人项目特定偏好 | 只有你（当前项目） |

### 设置项目 CLAUDE.md

运行 `/init` 自动生成起始 CLAUDE.md。Claude 分析你的代码库并创建包含构建命令、测试指令和项目约定的文件。

### 编写有效指令

**大小**：每个 CLAUDE.md 文件控制在 200 行以内。更长的文件消耗更多上下文并降低遵循度。

**结构**：使用 markdown 标题和项目符号对相关指令进行分组。

**具体性**：编写足够具体可验证的指令：
* "使用 2 空格缩进" 而不是 "正确格式化代码"
* "提交前运行 `npm test`" 而不是 "测试你的更改"
* "API 处理程序在 `src/api/handlers/`" 而不是 "保持文件有序"

### 导入其他文件

CLAUDE.md 文件可以使用 `@path/to/import` 语法导入其他文件：

```text
参见 @README 了解项目概述和 @package.json 了解可用的 npm 命令。

# 其他指令
- git 工作流程 @docs/git-instructions.md
```

### 使用 `.claude/rules/` 组织规则

对于较大的项目，可以将指令组织到 `.claude/rules/` 目录中的多个文件：

```text
your-project/
├── .claude/
│   ├── CLAUDE.md           # 主要项目指令
│   └── rules/
│       ├── code-style.md   # 代码风格指南
│       ├── testing.md      # 测试约定
│       └── security.md     # 安全要求
```

#### 路径特定规则

规则可以使用 `paths` 字段限定到特定文件：

```markdown
---
paths:
- "src/api/**/*.ts"
---
# API 开发规则
- 所有 API 端点必须包含输入验证
- 使用标准错误响应格式
- 包含 OpenAPI 文档注释
```

## 自动记忆

自动记忆让 Claude 跨会话积累知识，无需你编写任何内容。Claude 在工作时为自己保存笔记：构建命令、调试见解、架构说明、代码风格偏好和工作流程习惯。

### 启用或禁用自动记忆

自动记忆默认开启。要切换，在会话中打开 `/memory` 并使用自动记忆开关，或在项目设置中设置：

```json
{
  "autoMemoryEnabled": false
}
```

### 存储位置

每个项目都有自己的记忆目录 `~/.claude/projects/<project-hash>/memory/`：

```text
~/.claude/projects/<project-hash>/memory/
├── MEMORY.md          # 简洁索引，加载到每个会话
├── debugging.md       # 调试模式的详细说明
├── api-conventions.md # API 设计决策
└── ...                # Claude 创建的其他主题文件
```

### 工作原理

`MEMORY.md` 的前 200 行在每个对话开始时加载。超过 200 行的内容不会在会话开始时加载。Claude 通过将详细说明移动到单独的主题文件来保持 `MEMORY.md` 简洁。

## 使用 `/memory` 查看和编辑

`/memory` 命令列出当前会话中加载的所有 CLAUDE.md 和规则文件，让你开关自动记忆，并提供打开自动记忆文件夹的链接。选择任何文件在编辑器中打开它。

## 故障排除

### Claude 没有遵循我的 CLAUDE.md

* 运行 `/memory` 验证你的 CLAUDE.md 文件是否被加载
* 使指令更具体
* 查找 CLAUDE.md 文件中的冲突指令

### 我的 CLAUDE.md 太大

超过 200 行的文件消耗更多上下文，可能会降低遵循度。将详细内容移动到使用 `@path` 导入引用的单独文件中，或将指令拆分到 `.claude/rules/` 文件中。
