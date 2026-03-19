# 创建插件

> 创建自定义插件，用 skills、agents、hooks 和 MCP 服务器扩展 Claude Code。

插件让你用可跨项目和团队共享的自定义功能扩展 Claude Code。

## 何时使用插件 vs 独立配置

| 方式 | Skill 名称 | 最适合 |
|------|------------|--------|
| **独立配置** (`.claude/` 目录) | `/hello` | 个人工作流程、项目特定定制、快速实验 |
| **插件** (`.claude-plugin/plugin.json`) | `/plugin-name:hello` | 与团队共享、分发给社区、版本发布 |

**使用独立配置当：**
* 你为单个项目定制 Claude Code
* 配置是个人的，不需要共享
* 在打包前实验 skills 或 hooks
* 你想要短的 skill 名称如 `/hello` 或 `/deploy`

**使用插件当：**
* 你想与团队或社区共享功能
* 你需要跨多个项目使用相同的 skills/agents
* 你想要版本控制和易于更新
* 你通过 marketplace 分发

## 快速入门

### 创建你的第一个插件

```bash
# 创建插件目录
mkdir my-first-plugin
mkdir my-first-plugin/.claude-plugin
```

创建 `my-first-plugin/.claude-plugin/plugin.json`：

```json
{
  "name": "my-first-plugin",
  "description": "学习基础的问候插件",
  "version": "1.0.0",
  "author": {
    "name": "Your Name"
  }
}
```

创建 skill 目录和文件：

```bash
mkdir -p my-first-plugin/skills/hello
```

创建 `my-first-plugin/skills/hello/SKILL.md`：

```markdown
---
description: 用友好消息问候用户
disable-model-invocation: true
---
热情地问候用户，询问今天如何帮助他们。
```

### 测试插件

```bash
claude --plugin-dir ./my-first-plugin
```

在 Claude Code 中运行：

```
/my-first-plugin:hello
```

### 添加参数支持

更新 `SKILL.md`：

```markdown
---
description: 用个性化消息问候用户
---
# Hello Skill

热情地问候名为 "$ARGUMENTS" 的用户，询问今天如何帮助他们。让问候个性化和鼓舞人心。
```

运行：

```
/my-first-plugin:hello Alex
```

## 插件结构

```
my-plugin/
├── .claude-plugin/
│   └── plugin.json      # 插件清单
├── commands/            # Skills（Markdown 文件）
├── agents/              # 自定义代理定义
├── skills/              # Agent Skills（SKILL.md 文件）
├── hooks/
│   └── hooks.json       # 事件处理器
├── .mcp.json            # MCP 服务器配置
├── .lsp.json            # LSP 服务器配置
└── settings.json        # 默认设置
```

**常见错误**：不要把 `commands/`、`agents/`、`skills/` 或 `hooks/` 放在 `.claude-plugin/` 目录内。

## 开发更复杂的插件

### 添加 Skills

在插件根目录添加 `skills/` 目录：

```text
my-plugin/
├── .claude-plugin/
│   └── plugin.json
└── skills/
    └── code-review/
        └── SKILL.md
```

`SKILL.md` 示例：

```yaml
---
name: code-review
description: 审查代码的最佳实践和潜在问题
---

审查代码时，检查：
1. 代码组织和结构
2. 错误处理
3. 安全问题
4. 测试覆盖
```

### 添加 LSP 服务器

添加 `.lsp.json` 文件：

```json
{
  "go": {
    "command": "gopls",
    "args": ["serve"],
    "extensionToLanguage": {
      ".go": "go"
    }
  }
}
```

### 本地测试插件

```bash
claude --plugin-dir ./my-plugin
```

修改后运行 `/reload-plugins` 重新加载。

加载多个插件：

```bash
claude --plugin-dir ./plugin-one --plugin-dir ./plugin-two
```

### 调试插件问题

1. **检查结构**：确保目录在插件根目录，不在 `.claude-plugin/` 内
2. **单独测试组件**：分别检查每个命令、agent 和 hook
3. **使用验证工具**：参见调试文档

## 将现有配置转换为插件

### 迁移步骤

```bash
# 创建插件目录
mkdir -p my-plugin/.claude-plugin
```

创建 `my-plugin/.claude-plugin/plugin.json`：

```json
{
  "name": "my-plugin",
  "description": "从独立配置迁移",
  "version": "1.0.0"
}
```

复制现有配置：

```bash
# 复制 commands
cp -r .claude/commands my-plugin/
# 复制 agents（如果有）
cp -r .claude/agents my-plugin/
# 复制 skills（如果有）
cp -r .claude/skills my-plugin/
```

如果有 hooks，创建 `my-plugin/hooks/hooks.json`：

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [{ "type": "command", "command": "jq -r '.tool_input.file_path' | xargs npm run lint:fix" }]
      }
    ]
  }
}
```

验证：

```bash
claude --plugin-dir ./my-plugin
```

## 下一步

### 对于插件用户
* [发现和安装插件](/en/discover-plugins)
* [配置团队 marketplace](/en/discover-plugins#configure-team-marketplaces)

### 对于插件开发者
* [创建和分发 marketplace](/en/plugin-marketplaces)
* [插件参考](/en/plugins-reference)
* 深入了解特定组件：
  * [Skills](/en/skills)
  * [子代理](/en/sub-agents)
  * [Hooks](/en/hooks)
  * [MCP](/en/mcp)
