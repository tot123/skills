# Claude Code 概述

> Claude Code 是一个智能编程工具，可以阅读你的代码库、编辑文件、运行命令，并与你的开发工具集成。可在终端、IDE、桌面应用和浏览器中使用。

Claude Code 是一个 AI 驱动的编程助手，帮助你构建功能、修复错误和自动化开发任务。它能理解你的整个代码库，并可以跨多个文件和工具完成任务。

## 快速开始

选择你的环境开始使用。大多数平台需要 [Claude 订阅](https://claude.com/pricing) 或 [Anthropic Console](https://console.anthropic.com/) 账户。

### 终端 CLI

在终端中直接使用 Claude Code 的完整功能 CLI。编辑文件、运行命令，从命令行管理整个项目。

**安装方式：**

**macOS, Linux, WSL:**
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell:**
```powershell
irm https://claude.ai/install.ps1 | iex
```

**Windows CMD:**
```batch
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

> Windows 需要 [Git for Windows](https://git-scm.com/downloads/win)。请先安装。

**Homebrew (macOS):**
```bash
brew install --cask claude-code
```

**WinGet (Windows):**
```powershell
winget install Anthropic.ClaudeCode
```

然后在任何项目中启动：
```bash
cd your-project
claude
```

首次使用时会提示登录。

### VS Code 扩展

VS Code 扩展提供内联差异、@提及、计划审查和对话历史记录。

* [安装 VS Code 版](vscode:extension/anthropic.claude-code)
* [安装 Cursor 版](cursor:extension/anthropic.claude-code)

或在扩展视图 (`Cmd+Shift+X` / `Ctrl+Shift+X`) 中搜索 "Claude Code"。

### 桌面应用

在 IDE 或终端外运行 Claude Code 的独立应用。可视化审查差异、并行运行多个会话。

下载安装：
* [macOS](https://claude.ai/api/desktop/darwin/universal/dmg/latest/redirect) (Intel 和 Apple Silicon)
* [Windows](https://claude.ai/api/desktop/win32/x64/exe/latest/redirect) (x64)

### 网页版

在浏览器中运行 Claude Code，无需本地设置。处理长时间任务、在没有本地的仓库上工作，或并行运行多个任务。

开始使用：[claude.ai/code](https://claude.ai/code)

### JetBrains IDE

适用于 IntelliJ IDEA、PyCharm、WebStorm 等 JetBrains IDE 的插件。

从 JetBrains Marketplace 安装 [Claude Code 插件](https://plugins.jetbrains.com/plugin/27310-claude-code-beta-)。

## 功能特性

### 自动化日常任务

Claude Code 处理占用你时间的繁琐任务：为未测试的代码编写测试、修复项目中的 lint 错误、解决合并冲突、更新依赖、编写发布说明。

```bash
claude "为认证模块编写测试，运行它们，并修复任何失败"
```

### 自然语言描述功能

用简单的语言描述你想要什么。Claude Code 会规划方法、跨多个文件编写代码并验证其工作。

### Git 集成

Claude Code 直接与 git 配合使用。它暂存更改、编写提交消息、创建分支并打开拉取请求。

```bash
claude "用描述性消息提交我的更改"
```

### MCP 集成

[模型上下文协议 (MCP)](/en/mcp) 是连接 AI 工具与外部数据源的开放标准。使用 MCP，Claude Code 可以读取 Google Drive 中的设计文档、更新 Jira 中的工单、从 Slack 拉取数据或使用你自己的自定义工具。

### 项目记忆

[`CLAUDE.md`](/en/memory) 是添加到项目根目录的 markdown 文件，Claude Code 在每个会话开始时读取。用它设置编码标准、架构决策、首选库和审查清单。

### 自定义命令

创建[自定义命令](/en/skills)来打包可共享的重复工作流程，如 `/review-pr` 或 `/deploy-staging`。

### Hooks

[Hooks](/en/hooks) 让你在 Claude Code 操作之前或之后运行 shell 命令，如每次文件编辑后自动格式化或在提交前运行 lint。

### 多代理

生成[多个 Claude Code 代理](/en/sub-agents)，同时处理任务的不同部分。主导代理协调工作、分配子任务并合并结果。

## 下一步

* [快速入门](/en/quickstart)：完成第一个真实任务
* [存储指令和记忆](/en/memory)：使用 CLAUDE.md 文件给 Claude 持久指令
* [常见工作流程](/en/common-workflows) 和[最佳实践](/en/best-practices)
* [设置](/en/settings)：为你的工作流程自定义 Claude Code
* [故障排除](/en/troubleshooting)：常见问题的解决方案
