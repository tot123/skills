# Skills

Claude Code 技能插件集合，提供代码提交、评审、风格检查等功能。

## 安装

### 方式一：启动时指定插件目录（推荐）

```bash
# 克隆仓库
git clone https://github.com/tot123/skills.git ~/skills-code

# 启动 Claude Code 时指定插件目录
claude --plugin-dir ~/skills-code/code
```

### 方式二：复制到插件目录

```bash
# 克隆仓库
git clone https://github.com/tot123/skills.git ~/skills-code

# 复制到 Claude 插件目录
cp -r ~/skills-code/code ~/.claude/plugins/code
```

### 方式三：软链接

```bash
# 克隆仓库
git clone https://github.com/tot123/skills.git ~/skills-code

# 创建软链接
ln -s ~/skills-code/code ~/.claude/plugins/code
```

安装后重启 Claude Code 即可使用。

## 插件列表

### code - 代码提交与评审工具集

代码提交与评审工具集，遵循 Google 工程实践规范。

| 命令 | 说明 |
|------|------|
| `/code:push-diff` | 提交代码到远端代码库 |
| `/code:code-style` | 代码风格与质量检查 |
| `/code:code-review` | 代码评审 |
| `/code:code-review-fix` | 修复代码评审问题 |

#### 使用示例

```bash
# 提交代码变更
/code:push-diff

# 检查代码风格
/code:code-style

# 进行代码评审
/code:code-review

# 修复评审问题
/code:code-review-fix
```

## Google 提交规范

本插件遵循 [Google Engineering Practices](https://google.github.io/eng-practices/) 规范。

### 提交信息格式

```
<类型>: <简短摘要>

<详细说明为什么做这个变更>
```

### 首行规则

- 不超过 50 字符
- 使用祈使句（`Add feature` 而非 `Adding feature`）
- 首行后空一行

### 类型前缀

| 前缀 | 用途 |
|------|------|
| `feat` | 新功能 |
| `fix` | Bug 修复 |
| `refactor` | 重构 |
| `docs` | 文档 |
| `style` | 格式 |
| `test` | 测试 |
| `chore` | 构建/工具 |
| `perf` | 性能 |

### 示例

**好的提交：**

```
feat: Add user authentication module

Implement JWT-based authentication with refresh token support.
This enables secure API access and session management.
```

**不好的提交：**

```
Fix bug
Add patch
Phase 1
```

## 目录结构

```
.
├── README.md                   # 项目说明
├── CLAUDE.md                   # Claude 指导文档
├── claude-code-docs/           # Claude Code 中文文档
│   ├── overview.md             # 概述
│   ├── quickstart.md           # 快速入门
│   ├── skills.md               # Skills 使用指南
│   ├── memory.md               # 记忆和 CLAUDE.md
│   ├── hooks-guide.md          # Hooks 自动化指南
│   └── plugins.md              # 插件开发指南
├── company-coding-standards/   # 代码规范文档
│   ├── Google-*.md             # Google 各语言规范
│   ├── Alibaba-Java-规范.md    # 阿里巴巴 Java 规范
│   └── ...
└── code/                       # code 插件
    ├── .claude-plugin/
    │   └── plugin.json         # 插件配置
    └── commands/
        ├── push-diff.md        # 提交代码命令
        ├── code-style.md       # 风格检查命令
        ├── code-review.md      # 代码评审命令
        └── code-review-fix.md  # 修复问题命令
```

## 参考资源

- [Google Engineering Practices](https://google.github.io/eng-practices/)
- [Google Style Guides](https://google.github.io/styleguide/)
- [Conventional Commits](https://www.conventionalcommits.org/)
