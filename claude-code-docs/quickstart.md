# 快速入门

> 欢迎使用 Claude Code！

本快速入门指南将帮助你在几分钟内开始使用 AI 驱动的编程辅助。完成后，你将了解如何使用 Claude Code 完成常见的开发任务。

## 准备工作

确保你有：
* 打开的终端或命令提示符
* 一个代码项目
* [Claude 订阅](https://claude.com/pricing)（Pro、Max、Teams 或 Enterprise）或 [Claude Console](https://console.anthropic.com/) 账户

## 步骤 1：安装 Claude Code

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

> Windows 需要 [Git for Windows](https://git-scm.com/downloads/win)。

**Homebrew (macOS):**
```bash
brew install --cask claude-code
```

**WinGet (Windows):**
```powershell
winget install Anthropic.ClaudeCode
```

## 步骤 2：登录账户

Claude Code 需要账户才能使用：

```bash
claude
# 首次使用时会提示登录
```

可用的账户类型：
* [Claude Pro, Max, Teams, 或 Enterprise](https://claude.com/pricing)（推荐）
* [Claude Console](https://console.anthropic.com/)（API 访问）
* [Amazon Bedrock, Google Vertex AI, 或 Microsoft Foundry](/en/third-party-integrations)

## 步骤 3：开始第一个会话

在项目目录中打开终端并启动 Claude Code：

```bash
cd /path/to/your/project
claude
```

## 步骤 4：提出第一个问题

```text
这个项目是做什么的？
```

Claude 会分析你的文件并提供摘要。你也可以问更具体的问题：

```text
这个项目使用什么技术？
```

```text
主入口在哪里？
```

```text
解释文件夹结构
```

## 步骤 5：进行第一次代码更改

```text
在主文件中添加一个 hello world 函数
```

Claude Code 会：
1. 找到合适的文件
2. 显示建议的更改
3. 请求你的批准
4. 进行编辑

## 步骤 6：使用 Git

```text
我更改了哪些文件？
```

```text
用描述性消息提交我的更改
```

## 步骤 7：修复错误或添加功能

```text
为用户注册表单添加输入验证
```

或修复现有问题：

```text
有一个用户可以提交空表单的错误 - 修复它
```

## 步骤 8：测试其他常见工作流程

**重构代码**
```text
将认证模块重构为使用 async/await 而不是回调
```

**编写测试**
```text
为计算器函数编写单元测试
```

**更新文档**
```text
用安装说明更新 README
```

**代码审查**
```text
审查我的更改并提出改进建议
```

## 常用命令

| 命令 | 作用 | 示例 |
|------|------|------|
| `claude` | 启动交互模式 | `claude` |
| `claude "任务"` | 运行一次性任务 | `claude "修复构建错误"` |
| `claude -p "查询"` | 运行一次性查询后退出 | `claude -p "解释这个函数"` |
| `claude -c` | 继续当前目录最近的对话 | `claude -c` |
| `claude -r` | 恢复之前的对话 | `claude -r` |
| `claude commit` | 创建 Git 提交 | `claude commit` |
| `/clear` | 清除对话历史 | `/clear` |
| `/help` | 显示可用命令 | `/help` |

## 新手专业提示

### 提供具体细节

不要说："修复错误"
尝试说："修复用户输入错误凭据后看到空白屏幕的登录错误"

### 分解复杂任务

```text
1. 为用户配置文件创建新的数据库表
2. 创建获取和更新用户配置文件的 API 端点
3. 构建一个允许用户查看和编辑其信息的网页
```

### 让 Claude 先理解代码

```text
分析数据库架构
```

### 使用键盘快捷键

* 按 `?` 查看所有可用的键盘快捷键
* 使用 Tab 进行命令补全
* 按 ↑ 查看命令历史
* 输入 `/` 查看所有命令和技能

## 下一步

* [工作原理](/en/how-claude-code-works)：了解智能循环、内置工具
* [最佳实践](/en/best-practices)：通过有效提示和项目设置获得更好结果
* [常见工作流程](/en/common-workflows)：常见任务的分步指南
* [扩展 Claude Code](/en/features-overview)：使用 CLAUDE.md、技能、钩子、MCP 等

## 获取帮助

* **在 Claude Code 中**：输入 `/help` 或问"我如何..."
* **文档**：浏览其他指南
* **社区**：加入我们的 [Discord](https://www.anthropic.com/discord)
