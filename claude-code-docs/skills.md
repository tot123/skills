# 使用 Skills 扩展 Claude

> 创建、管理和共享 skills 来扩展 Claude 在 Claude Code 中的功能。

Skills 扩展了 Claude 的能力。创建一个 `SKILL.md` 文件，Claude 就会将其添加到工具箱中。Claude 在相关时使用 skills，或者你可以直接用 `/skill-name` 调用。

## 内置 Skills

以下 skills 随 Claude Code 一起提供，在每个会话中都可用：

| Skill | 用途 |
|-------|------|
| `/batch <任务>` | 在代码库中并行编排大规模更改 |
| `/claude-api` | 加载 Claude API 参考资料和 Agent SDK 参考 |
| `/debug [描述]` | 通过读取会话调试日志排查当前会话问题 |
| `/loop [间隔] <提示>` | 按间隔重复运行提示 |
| `/simplify [重点]` | 审查最近更改的文件并修复问题 |

## 创建你的第一个 Skill

### 1. 创建 Skill 目录

在个人 skills 文件夹中创建目录。个人 skills 在所有项目中都可用：

```bash
mkdir -p ~/.claude/skills/explain-code
```

### 2. 创建 SKILL.md 文件

每个 skill 需要一个 `SKILL.md` 文件，包含两部分：YAML frontmatter（在 `---` 标记之间）和 markdown 内容。

创建 `~/.claude/skills/explain-code/SKILL.md`：

```yaml
---
name: explain-code
description: 使用可视化和类比解释代码。当解释代码如何工作或用户问"这是如何工作的？"时使用
---

解释代码时，始终包括：
1. **从类比开始**：将代码与日常生活进行比较
2. **画图**：使用 ASCII 艺术显示流程、结构或关系
3. **逐步讲解**：逐步解释发生了什么
4. **强调陷阱**：常见的错误或误解是什么？
```

### 3. 测试 Skill

**让 Claude 自动调用**：
```text
这段代码是如何工作的？
```

**或直接调用**：
```text
/explain-code src/auth/login.ts
```

## Skills 存放位置

| 位置 | 路径 | 适用范围 |
|------|------|----------|
| 企业 | 参见托管设置 | 组织中的所有用户 |
| 个人 | `~/.claude/skills/<name>/SKILL.md` | 你的所有项目 |
| 项目 | `.claude/skills/<name>/SKILL.md` | 仅此项目 |
| 插件 | `<plugin>/skills/<name>/SKILL.md` | 插件启用的地方 |

当 skills 在不同级别共享相同名称时，优先级为：企业 > 个人 > 项目。

## Skill 目录结构

```text
my-skill/
├── SKILL.md          # 主要指令（必需）
├── template.md       # Claude 填写的模板
├── examples/
│   └── sample.md     # 显示预期格式的示例输出
└── scripts/
    └── validate.sh   # Claude 可以执行的脚本
```

## Frontmatter 配置

```yaml
---
name: my-skill
description: 这个 skill 做什么
disable-model-invocation: true
allowed-tools: Read, Grep
---
```

| 字段 | 必需 | 描述 |
|------|------|------|
| `name` | 否 | Skill 的显示名称，用作 `/命令` |
| `description` | 推荐 | Skill 做什么以及何时使用 |
| `disable-model-invocation` | 否 | 设为 `true` 阻止 Claude 自动加载此 skill |
| `user-invocable` | 否 | 设为 `false` 从 `/` 菜单隐藏 |
| `allowed-tools` | 否 | 此 skill 激活时 Claude 无需询问权限即可使用的工具 |
| `context` | 否 | 设为 `fork` 在分叉的子代理上下文中运行 |
| `agent` | 否 | 当设置 `context: fork` 时使用的子代理类型 |

## 参数传递

使用 `$ARGUMENTS` 占位符传递参数：

```yaml
---
name: fix-issue
description: 修复 GitHub issue
disable-model-invocation: true
---
修复 GitHub issue $ARGUMENTS，遵循我们的编码标准。
1. 阅读 issue 描述
2. 理解需求
3. 实现修复
4. 编写测试
5. 创建提交
```

运行 `/fix-issue 123`，Claude 会收到 "修复 GitHub issue 123..."

## 控制谁可以调用 Skill

| Frontmatter | 你可以调用 | Claude 可以调用 |
|-------------|-----------|----------------|
| (默认) | 是 | 是 |
| `disable-model-invocation: true` | 是 | 否 |
| `user-invocable: false` | 否 | 是 |

## 在子代理中运行 Skills

添加 `context: fork` 到 frontmatter，让 skill 在隔离环境中运行：

```yaml
---
name: deep-research
description: 彻底研究一个主题
context: fork
agent: Explore
---
彻底研究 $ARGUMENTS：
1. 使用 Glob 和 Grep 查找相关文件
2. 阅读和分析代码
3. 用具体文件引用总结发现
```

## 动态上下文注入

使用 `!`command`` 语法在 skill 内容发送给 Claude 之前运行 shell 命令：

```yaml
---
name: pr-summary
description: 总结拉取请求中的更改
context: fork
agent: Explore
allowed-tools: Bash(gh *)
---
## 拉取请求上下文
- PR 差异: !`gh pr diff`
- PR 评论: !`gh pr view --comments`
- 更改的文件: !`gh pr diff --name-only`

## 你的任务
总结这个拉取请求...
```

## 插件中使用 Skills

插件可以包含 skills 目录：

```text
my-plugin/
├── .claude-plugin/
│   └── plugin.json
└── skills/
    └── my-skill/
        └── SKILL.md
```

插件中的 skills 使用 `plugin-name:skill-name` 命名空间，因此不会与其他级别的 skills 冲突。

## 故障排除

### Skill 没有触发

1. 检查描述是否包含用户会自然说的关键词
2. 验证 skill 是否出现在 `/help` 中
3. 尝试重新表述你的请求以更匹配描述
4. 如果 skill 是用户可调用的，直接用 `/skill-name` 调用

### Skill 触发太频繁

1. 使描述更具体
2. 如果你只想手动调用，添加 `disable-model-invocation: true`

### Claude 没有看到所有 skills

Skill 描述被加载到上下文中。如果你有很多 skills，可能会超出字符预算。运行 `/context` 检查是否有关于被排除 skills 的警告。
