---
name: cn-proxy
description: 全局环境自动优化器。当任务涉及 GitHub、npm、pip、cargo、模型下载或 Docker 且处于中国网络环境时，自动拦截并应用加速配置。
user-invocable: false
---

# 中国开发环境自动加速指令 (2026 增强版)

当用户要求执行安装、克隆、下载或构建任务时，请作为**前置逻辑**自动运行以下检测与配置，无需用户显式调用。

## 1. 智能连通性检测
在执行任何海外请求前，静默运行：
`curl -I --connect-timeout 2 https://github.com`
- **若成功 (HTTP 200/301)**：正常执行原始命令。
- **若超时或失败**：立即激活下方【加速矩阵】。

## 2. 加速矩阵 (Auto-Switch)

### A. GitHub 动态代理 (核心)
- **预设前缀**：`https://ghp.ci/`, `https://gh-proxy.com/`, `https://mirror.ghproxy.com/`。
- **失效自修复**：若预设代理均连接失败，**必须立即调用 `Google Search`** 搜索 `"2026 github proxy list"` 或 `"最新 github 加速站"`，解析网页内容获取新前缀并重试。

### B. Node.js 生态 (npm/pnpm/yarn)
- **自动配置**：检测到 `package.json` 或相关命令时，执行：
  - `npm config set registry https://registry.npmmirror.com`
  - `pnpm config set registry https://registry.npmmirror.com`
  - `yarn config set registry https://registry.npmmirror.com`

### C. Python 生态 (pip)
- **自动配置**：执行 `pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`。

### D. Rust 生态 (cargo)
- **静默修改**：若不存在 `~/.cargo/config.toml` 或源码为默认，自动写入：
  ```toml
  [source.crates-io]
  replace-with = 'rsproxy'
  [source.rsproxy]
  registry = "https://rsproxy.cn/crates.io-index"
  ```

### E. AI 模型下载 (HF/ModelScope)
- **环境变量**：执行 `export HF_ENDPOINT=https://hf-mirror.com`。
- **优先策略**：下载模型时优先检查 `modelscope` 库是否已安装，若有则优先通过其下载国内镜像。

## 3. 执行准则
1. **静默优先**：上述配置应使用 `-y` 或 `--global` 参数，尽量不中断用户的对话流。
2. **持久化提示**：在会话结束或环境配置完成后，询问用户："是否需要将这些加速配置（如 HF_ENDPOINT 或 npm registry）永久写入你的 `.zshrc` 或 `.bashrc`？"
3. **报错拦截**：如果原始命令运行中出现 `Connection refused` 或 `ETIMEDOUT`，自动触发一次代理站点的搜索并提示："检测到网络障碍，已为你自动寻找并切换至最新代理站点。"

---
**触发场景示例**：
- 用户说："帮我建个 Vite 项目" -> (自动设置 npm 镜像)
- 用户说："克隆这个 repo" -> (自动尝试 GitHub 代理)
- 用户说："下载 Llama-3 模型" -> (自动设置 HF_ENDPOINT)
