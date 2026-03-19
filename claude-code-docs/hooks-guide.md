# 使用 Hooks 自动化工作流程

> 当 Claude Code 编辑文件、完成任务或需要输入时自动运行 shell 命令。格式化代码、发送通知、验证命令并执行项目规则。

Hooks 是在 Claude Code 生命周期特定点执行的用户定义 shell 命令。它们提供对 Claude Code 行为的确定性控制，确保某些操作始终发生，而不是依赖 LLM 选择运行它们。

## 设置你的第一个 Hook

在 Claude Code 中通过 `/hooks` 交互菜单创建 hook 最快。

1. 在 Claude Code CLI 中输入 `/hooks`
2. 选择 `Notification` 事件
3. 将 matcher 设置为 `*`
4. 选择 `+ Add new hook…`
5. 输入你的 shell 命令
6. 选择保存位置（用户设置或项目设置）

**macOS 通知命令：**
```bash
osascript -e 'display notification "Claude Code needs your attention" with title "Claude Code"'
```

**Linux 通知命令：**
```bash
notify-send 'Claude Code' 'Claude Code needs your attention'
```

**Windows 通知命令：**
```powershell
powershell.exe -Command "[System.Reflection.Assembly]::LoadWithPartialName('System.Windows.Forms'); [System.Windows.Forms.MessageBox]::Show('Claude Code needs your attention', 'Claude Code')"
```

## 你可以自动化什么

### 在 Claude 需要输入时获得通知

添加到 `~/.claude/settings.json`：

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Claude Code needs your attention\" with title \"Claude Code\"'"
          }
        ]
      }
    ]
  }
}
```

### 编辑后自动格式化代码

添加到 `.claude/settings.json`：

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "jq -r '.tool_input.file_path' | xargs npx prettier --write"
          }
        ]
      }
    ]
  }
}
```

### 阻止编辑受保护文件

创建 `.claude/hooks/protect-files.sh`：

```bash
#!/bin/bash
INPUT=$(cat)
FILE_PATH=$(echo "$INPUT" | jq -r '.tool_input.file_path // empty')
PROTECTED_PATTERNS=(".env" "package-lock.json" ".git/")

for pattern in "${PROTECTED_PATTERNS[@]}"; do
  if [[ "$FILE_PATH" == *"$pattern"* ]]; then
    echo "Blocked: $FILE_PATH matches protected pattern '$pattern'" >&2
    exit 2
  fi
done
exit 0
```

添加 hook 配置：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/protect-files.sh"
          }
        ]
      }
    ]
  }
}
```

## Hook 事件

| 事件 | 何时触发 |
|------|----------|
| `SessionStart` | 会话开始或恢复时 |
| `UserPromptSubmit` | 提交提示时，Claude 处理之前 |
| `PreToolUse` | 工具调用执行前，可阻止 |
| `PermissionRequest` | 权限对话框出现时 |
| `PostToolUse` | 工具调用成功后 |
| `PostToolUseFailure` | 工具调用失败后 |
| `Notification` | Claude Code 发送通知时 |
| `Stop` | Claude 完成响应时 |
| `ConfigChange` | 配置文件在会话中更改时 |
| `SessionEnd` | 会话终止时 |

## Hook 输入和输出

### 输入

Hook 通过 stdin 接收 JSON 数据：

```json
{
  "session_id": "abc123",
  "cwd": "/Users/sarah/myproject",
  "hook_event_name": "PreToolUse",
  "tool_name": "Bash",
  "tool_input": {
    "command": "npm test"
  }
}
```

### 输出

通过退出码控制行为：

* **Exit 0**：操作继续
* **Exit 2**：操作被阻止（stderr 作为反馈发送给 Claude）
* **其他退出码**：操作继续，stderr 被记录

## 配置 Hook 位置

| 位置 | 范围 |
|------|------|
| `~/.claude/settings.json` | 所有项目 |
| `.claude/settings.json` | 单个项目 |
| `.claude/settings.local.json` | 单个项目（不提交） |

## 故障排除

### Hook 没有触发

* 运行 `/hooks` 确认 hook 出现在正确事件下
* 检查 matcher 模式是否完全匹配工具名称
* 验证你触发了正确的事件类型

### Hook 错误

* 使用示例 JSON 手动测试脚本
* 使用绝对路径或 `$CLAUDE_PROJECT_DIR`
* 确保脚本可执行：`chmod +x ./my-hook.sh`
